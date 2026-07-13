# 16. File Processing Services

## File Watcher

Using `FileSystemWatcher` to react immediately when files are created/changed/deleted/renamed in a directory — an event-driven approach (no polling delay).

```csharp
public class FileWatcherWorker : BackgroundService
{
    private readonly ILogger<FileWatcherWorker> _logger;
    private FileSystemWatcher? _watcher;

    public FileWatcherWorker(ILogger<FileWatcherWorker> logger) => _logger = logger;

    protected override Task ExecuteAsync(CancellationToken stoppingToken)
    {
        _watcher = new FileSystemWatcher(@"C:\Incoming")
        {
            Filter = "*.csv",
            NotifyFilter = NotifyFilters.FileName | NotifyFilters.LastWrite,
            EnableRaisingEvents = true
        };

        _watcher.Created += OnFileCreated;
        _watcher.Error += (s, e) => _logger.LogError(e.GetException(), "FileSystemWatcher error");

        stoppingToken.Register(() => _watcher?.Dispose());
        return Task.CompletedTask;
    }

    private void OnFileCreated(object sender, FileSystemEventArgs e)
    {
        _logger.LogInformation("New file detected: {path}", e.FullPath);
        // Hand off to a queue/consumer rather than processing directly in the event handler
    }
}
```

⚠️ **Caveats with `FileSystemWatcher`:**
- Can **miss events** under heavy load (its internal buffer can overflow) — handle the `Error` event and consider a periodic reconciliation poll as a safety net.
- Fires the `Created` event before the writer has necessarily finished writing the file — you often need a "file is stable" check (e.g., try to open it exclusively, or wait until file size stops changing) before processing.
- Network drives/SFTP-mounted folders can behave unreliably with watchers — polling may be more robust there.

## File Polling

A simpler, more robust alternative for many real-world cases (especially network shares, SFTP-mounted directories): periodically scan the directory for new files.

```csharp
protected override async Task ExecuteAsync(CancellationToken stoppingToken)
{
    using var timer = new PeriodicTimer(TimeSpan.FromSeconds(30));

    while (await timer.WaitForNextTickAsync(stoppingToken))
    {
        var files = Directory.GetFiles(_incomingPath, "*.csv");
        foreach (var file in files)
        {
            if (IsFileReady(file))
            {
                await ProcessFileAsync(file, stoppingToken);
                File.Move(file, Path.Combine(_processedPath, Path.GetFileName(file)));
            }
        }
    }
}

private bool IsFileReady(string path)
{
    try
    {
        using var stream = File.Open(path, FileMode.Open, FileAccess.Read, FileShare.None);
        return true; // no other process has it open for writing
    }
    catch (IOException) { return false; }
}
```

## File Parsing

After detecting a file, you need to read and interpret its contents. The right approach depends on format.

### CSV Processing
```csharp
using var reader = new StreamReader(filePath);
string? line;
bool isHeader = true;
while ((line = await reader.ReadLineAsync()) != null)
{
    if (isHeader) { isHeader = false; continue; }
    var fields = line.Split(',');
    // map fields to a model, validate, persist
}
```
For more robust CSV handling (quoted fields, embedded commas, type conversion), use a library like **CsvHelper** rather than naive `Split(',')`.

### XML Processing
```csharp
using var stream = File.OpenRead(filePath);
var doc = XDocument.Load(stream);
var records = doc.Descendants("Record")
    .Select(r => new MyRecord
    {
        Id = (string)r.Element("Id"),
        Amount = (decimal)r.Element("Amount")
    });
```

### JSON Processing
```csharp
using var stream = File.OpenRead(filePath);
var records = await JsonSerializer.DeserializeAsync<List<MyRecord>>(stream, cancellationToken: stoppingToken);
```

### Fixed-Width / Custom Formats (Common in Banking Files)
```csharp
string line = "...";
string accountNumber = line.Substring(0, 15).Trim();
string amount = line.Substring(15, 10).Trim();
string transactionType = line.Substring(25, 2).Trim();
```
Fixed-width parsing requires precise knowledge of the byte offsets specified by the file format documentation provided by the bank/partner.

---

## ACH File Processing
ACH (Automated Clearing House — US banking) files follow the **NACHA** fixed-width file format, with specific record types (File Header, Batch Header, Entry Detail, Batch Control, File Control). A background service responsible for ACH typically:
1. Generates outgoing ACH files from pending transaction records in the DB, following the exact record-type layout and checksum/control totals required.
2. Transmits the file to the bank (SFTP, API, or direct submission portal).
3. Polls for/receives acknowledgment and return files (e.g., NOC — Notification of Change, or returned/rejected transactions).
4. Parses returned files and updates transaction statuses in the DB, triggering any necessary business workflows (e.g., notify the customer of a failed debit).

## NACH File Processing
NACH (National Automated Clearing House — Indian banking equivalent, run by NPCI) follows a similar conceptual flow but with India-specific file formats and registrars (mandate registration files, debit/credit instruction files, response files). A background service for NACH typically:
1. **Mandate Registration** — generates and submits mandate registration request files to the sponsor bank/NPCI.
2. **Debit/Credit File Generation** — on each cycle (e.g., daily or per due date), pulls due EMI/subscription records, generates the prescribed fixed-format debit file.
3. **Submission** — uploads to the bank's SFTP or portal within the cutoff window.
4. **Response Processing** — downloads and parses response files (success/failure per record, with bank-specific reason codes), updates the local DB, and triggers downstream actions (retry, dunning notifications, ledger updates).
5. **Reconciliation** — cross-checks submitted vs. responded counts/amounts to catch any missing or mismatched records (see also Section 30 — Reconciliation Services).

### Why These Are "Background Service" Candidates
- They run on **fixed schedules** tied to bank cutoff times (Scheduled Jobs pattern).
- They involve **file I/O, SFTP transfer, and parsing** that shouldn't block any user-facing request.
- They require **robust error handling and retry** (a failed SFTP upload shouldn't silently lose a day's transactions).
- They often need **idempotency** — if the service restarts mid-run, it must not double-submit the same batch.

### Practical Safeguards for File-Based Banking Background Services
- Track file generation/submission status in a DB table (`Pending`, `Generated`, `Submitted`, `Acknowledged`, `Failed`) so restarts can resume safely rather than reprocessing blindly.
- Use atomic file moves (`File.Move` after processing, not delete-then-recreate) to avoid partial-state files.
- Log file checksums/record counts at each stage for auditability — critical in regulated financial workflows.
- Always wrap SFTP/network operations in retry logic with backoff (see Resilience Patterns section).