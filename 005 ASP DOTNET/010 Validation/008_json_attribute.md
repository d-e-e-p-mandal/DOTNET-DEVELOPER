

## JSON ATTRIBUTES (REQUEST + RESPONSE CONTROL)

**Namespace:**
```cs
using System.Text.Json.Serialization;
```


**JSON ATTRIBUTES :**
```cs
[JsonPropertyName("name")]   // change JSON name (request + response)

[JsonIgnore]  // ignore in request + response

[JsonInclude]  // include private fields

[JsonConverter(typeof(MyConverter))]  // custom conversion

[JsonNumberHandling(JsonNumberHandling.AllowReadingFromString)]  // allow "1000" as string → int

[JsonPropertyOrder(1)]  // control JSON output order
```


##### JSON ADVANCED (MISSING IMPORTANT)
```cs
[JsonIgnore(Condition = JsonIgnoreCondition.WhenWritingNull)]
// ignore only when null
[JsonIgnore(Condition = JsonIgnoreCondition.WhenWritingDefault)]
// ignore default values (0, null, false)
```