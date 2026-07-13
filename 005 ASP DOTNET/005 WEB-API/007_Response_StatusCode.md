[Response Type]() | [All Predefined]() | [Empty Special]() | [Custom Response Code]()

# ASP.NET CORE – RETURN TYPES 

Controller → returns IActionResult → ASP.NET converts to HTTP Response

**Example: :**
```cs
return Ok(data);
```
**Internally becomes :**
- HTTP/1.1 200 OK
- Content-Type: application/json
- { data }

**ASP.NET gives helper methods for each. :**


### REAL LIFE MAPPING

**GET :**
```cs
return Ok(data);      // 200
return NotFound();    // 404
```
- Meaning: Fetch data 

**POST :**
```cs
return CreatedAtAction(...); // 201
```
- Meaning: New resource created :


**PUT :**
```cs
return NoContent(); // 204
```
- Meaning: Updated successfully


**DELETE :**
```cs
return NoContent(); // 204
```
- Meaning: Deleted successfully :


### 6. WHEN TO USE EACH

**Use Ok() :**
* Returning data
* GET APIs

**Use CreatedAtAction() :**
* POST APIs
* Resource created

**Use NoContent() :**
* PUT / DELETE
* No response needed

**Use BadRequest() :**
* Validation fails

**Use NotFound() :**
* Resource missing

**Use StatusCode() :**
* Custom cases


### 7. INTERNAL FLOW (IMPORTANT)
```
Controller Method
   ↓
Return IActionResult
   ↓
Framework maps to HTTP status
   ↓
Response sent to client
```

### 8. FINAL SIMPLIFIED TABLE

Ok()              → 200 → success  
Created()         → 201 → created  
Accepted()        → 202 → processing  
NoContent()       → 204 → no data  
BadRequest()      → 400 → invalid  
Unauthorized()    → 401 → login required  
Forbid()          → 403 → no permission  
NotFound()        → 404 → not found  
Conflict()        → 409 → duplicate  
Unprocessable     → 422 → validation  
StatusCode()      → custom  
Content()         → text  
JsonResult        → JSON  
File()            → file  
Redirect()        → redirect  
EmptyResult       → empty  
ObjectResult      → manual control  


GET    → Ok / NotFound  
POST   → CreatedAtAction  
PUT    → NoContent  
DELETE → NoContent  

---------------------------------------------



## ALL PREDEFINED RETURN TYPE FUNCTIONS


### SUCCESS RESPONSES (2xx)


**`Ok()` :**
```cs
return Ok(object value);     // 200
return Ok();                 // 200
```
- Meaning: Success with/without data

**`Created()` :**
```cs
return Created(string uri, object value); // 201
```
- Meaning: Resource created with manual URL

**`CreatedAtAction()` :**
```cs
return CreatedAtAction(string action, object routeValues, object value);
```
- Meaning: 201 + auto URL (best for POST)

**`CreatedAtRoute()` :**
```cs
return CreatedAtRoute(string route, object routeValues, object value);
```
- Meaning: 201 + route-based URL

**`Accepted()` :**
```cs
return Accepted();               // 202
return Accepted(object value);   // 202
```
- Meaning: Accepted, processing later

**`AcceptedAtAction()` :**

```cs
return AcceptedAtAction(string action, object routeValues, object value);
```
- Meaning: Async processing reference

**`AcceptedAtRoute()` :**
```cs
return AcceptedAtRoute(string route, object routeValues, object value```);
```
- Meaning: Async + route

**`NoContent()` :**
```cs
return NoContent(); // 204
```
- Meaning: Success, no response body

### CLIENT ERROR RESPONSES (4xx)

**`BadRequest()` :**
```cs
return BadRequest();               // 400
return BcsadRequest(object error);   // 400
```

**`Unauthorized()` :**
```cs
return Unauthorized(); // 401
```

**`Forbid()` :**
```cs
return Forbid(); // 403
```

**`NotFound()` :**
```cs
return NotFound();               // 404
return NotFound(object value);   // 404
```

**`Conflict()` :**
```cs
return Conflict();               // 409
return Conflict(object value);   // 409
```

**`UnprocessableEntity()` :**
```cs
return UnprocessableEntity();               // 422
return UnprocessableEntity(object error);   // 422
```

**`ValidationProblem()` :**
```cs
return ValidationProblem(ModelState);
```
- Meaning: Standard validation error response

**`Problem()` :**
```cs
return Problem("Something went wrong");
```
- Meaning: RFC 7807 error response

### REDIRECTION RESPONSES (3xx)

🔁 Redirect()
```cs
return Redirect(string url); // 302
```

**`RedirectPermanent()`**
```cs
return RedirectPermanent(string url); // 301
```

**`RedirectToAction()`**
```cs
return RedirectToAction(string action);
```

**`RedirectToRoute()`**
```cs
return RedirectToRoute(string route);
```

**`LocalRedirect()`**
```cs
return LocalRedirect(string url);
```

**`LocalRedirectPermanent()`**
```cs
return LocalRedirectPermanent(string url);
```

---------------------------------------

### CONTENT / DATA RESPONSES

📄 Content()
```cs
return Content(string text);
return Content(string text, string contentType);
```

📦 JsonResult
```cs
return new JsonResult(object data);
```

📁 File() (ALL VARIANTS)
```cs
return File(byte[] data, string contentType);
return File(Stream stream, string contentType);
return File(string path, string contentType);
return PhysicalFile(string path, string contentType);
return VirtualFile(string path, string contentType);
```

------------------------------------


### 6. EMPTY / SPECIAL


📭 EmptyResult
```cs
return new EmptyResult();
```

📭 Challenge()
```cs
return Challenge(); // 401
```

📭 Forbid() (already above)


📭 SignIn()
```cs
return SignIn(principal, scheme);
```

📭 SignOut()
```cs
return SignOut();
```

### 7. PARTIAL / VIEW (MVC ONLY)


🧾 View()
```cs
return View(model);
```

🧾 PartialView()
```cs
return PartialView(model);
```

### 8. FILE DOWNLOAD ADVANCED


📁 FileContentResult

📁 FileStreamResult

📁 VirtualFileResult

📁 PhysicalFileResult

- All are internal types returned by File() helpers

**COMPLETE MASTER SUMMARY :**
200 → Ok  
201 →``` Created / CreatedAtAction / CreatedAtRoute  
202 → Accepted / AcceptedAtAction / AcceptedAtRoute  
204 → NoContent  
400 → Ba```csdRequest / ValidationProblem  
401 → Unauthorized / Challenge  
403 → Forbid ``` 
404 → NotFound  
409 → Conflict  
422 → UnprocessableEntity  
500 → StatusCode / Problem  
3xx → Redirect / RedirectToAction / RedirectToRoute  
Other → Content / Json / File / Empty / View  


-------------------------------------------------

### SERVER / CUSTOM RESPONSES

**`StatusCode()` :**
```cs
return StatusCode(int code);
return StatusCode(int code, object value); // custom status code set
```

**`ObjectResult` :**
```cs
return new ObjectResult(object value)
{
    StatusCode = 500  // custom status code set
};
```