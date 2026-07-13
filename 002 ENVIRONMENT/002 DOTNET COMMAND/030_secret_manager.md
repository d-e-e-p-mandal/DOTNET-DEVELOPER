# Secret Manager Command

```bash

dotnet user-secrets init

```

---

# Add Secret

```bash

dotnet user-secrets set "ApiKey" "12345"

```

---

# Read Secret

```cs

builder.Configuration["ApiKey"];

```