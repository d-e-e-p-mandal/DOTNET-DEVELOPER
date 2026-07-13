
======
## Read Variable

**IConfiguration:**
      ↓
Read Directly


**IOptions<T>**
      ↓
Read Once


**IOptionsSnapshot<T>**
      ↓
Read Every Request


**IOptionsMonitor<T>**
      ↓
Read Every Change


=======

## Working Type

**IConfiguration**
      ↓
Read Directly


**IOptions<T>**
      ↓
Read Once

**IOptionsSnapshot<T>**
      ↓
Read Every Request


**IOptionsMonitor<T>**
      ↓
Read Every Change



## Large Project

```text
IOptions<T>
```

## Background Service

```text
IOptionsMonitor<T>
```
