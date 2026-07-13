# Secret Manager
Secret Manager stores sensitive data safely during development.

**Used For:**
- Database passwords
- API keys
- JWT secrets
- Avoid storing secrets inside: appsettings.json

---

### Secret Manager Command
```bash
dotnet user-secrets init
```

**Add Secret:**
```bash
dotnet user-secrets set "ApiKey" "12345"
```


**Read Secret:**

```cs
builder.Configuration["ApiKey"];
```

### Example Priority

```text
appsettings.json
        ↓
appsettings.Development.json
        ↓
Environment Variables
        ↓
Secret Manager
```