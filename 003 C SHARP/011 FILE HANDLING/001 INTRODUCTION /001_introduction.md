## 1. Introduction to File Handling

### What is File Handling
- File Handling is the process of creating, reading, writing, updating, and deleting files using a programming language.

- It allows applications to store and retrieve data permanently from storage devices.

Common operations:

- Create File
- Read File
- Write File
- Update File
- Delete File

Example Uses:

- Store student records
- Save employee information
- Generate reports
- Store application logs
- Upload and download files

---

### File System Basics

- A File System is the method used by the operating system to organize and manage files and folders.

- It helps users and applications store, locate, and access data efficiently.

**Example Structure:**

```text
C:
│
├── Documents
│      ├── Resume.pdf
│      ├── Notes.txt
│
├── Images
│      ├── Photo.jpg
```

Purpose:

- Organize files
- Manage folders
- Store data
- Locate files quickly

---

### File vs Directory

#### File

A File is a collection of data stored on a storage device.

Examples:

```text
Resume.pdf
Notes.txt
Image.jpg
Data.json
Employee.xlsx
```

**Characteristics:**

- Stores data
- Has a file extension
- Can be opened, read, and modified


#### Directory (Folder)

- A Directory is a container used to store files and other directories.

**Examples:**

```text
Documents
Images
Projects
Downloads
```

**Characteristics:**

- Organizes files
- Can contain subfolders
- Helps manage data efficiently


#### Difference

| File | Directory |
|--------|-----------|
| Stores data | Stores files and folders |
| Has extension | Usually no extension |
| Contains content | Contains files/folders |
| Example: Resume.pdf | Example: Documents |

---

### Absolute Path

- An Absolute Path is the complete path from the root directory to a file or folder.

Example (Windows):

```text
C:\Users\Deep\Documents\Resume.pdf
```

Example (Linux/Mac):

```text
/home/deep/Documents/Resume.pdf
```

Characteristics:

- Complete location
- Starts from root directory
- Independent of current folder

Advantages:

- Always points to the same file
- No dependency on current location

---

### Relative Path

- A Relative Path is a path based on the current working directory.

Current Directory:

```text
C:\Projects\MyApp
```

File Location:

```text
C:\Projects\MyApp\Data\Employee.txt
```

Relative Path:

```text
Data\Employee.txt
```

Characteristics:

- Shorter path
- Depends on current directory
- Easier to move projects between systems

Examples:

```text
Data\Employee.txt

Images\Photo.jpg

Logs\Error.txt
```

---

### Absolute Path vs Relative Path

| Absolute Path | Relative Path |
|--------------|--------------|
| Full file location | Location relative to current folder |
| Starts from root | Starts from current directory |
| Independent of location | Depends on current location |
| Longer | Shorter |

Example:

Absolute Path

```text
C:\Projects\MyApp\Data\Employee.txt
```

Relative Path

```text
Data\Employee.txt
```