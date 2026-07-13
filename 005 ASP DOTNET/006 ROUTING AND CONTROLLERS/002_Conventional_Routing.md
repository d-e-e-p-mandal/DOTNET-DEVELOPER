-- (* not used in industry level)
-- (not recomended )

## Conventional Routing : 

Program.cs (Routing Setup)
```cs 
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllersWithViews();

var app = builder.Build();

// Conventional Routing
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}"
);

app.Run();
```
- `name` : this is label
- `pattern` : route mapping


Controllers/ProductController.cs
```cs
using Microsoft.AspNetCore.Mvc;

public class ProductController : Controller
{
    // GET request
    [HttpGet]
    // URL: /Product/List
    public IActionResult List()
    {
        return Content("Product List Page");
    }

    // URL: /Product/Details/5
    public IActionResult Details(int id)
    {
        return Content($"Product Details for ID = {id}");
    }
}
```

Create HomeController (Default)
```cs
using Microsoft.AspNetCore.Mvc;

public class HomeController : Controller
{
    // URL: /
    public IActionResult Index()
    {
        return Content("Welcome to Home Page");
    }
}
```

*Default URL:* http://localhost:5000/ 
Output: Welcome to Home Page

*Product Details:* http://localhost:5000/Product/Details/10
Output: Product Details for ID = 10


---
##### Alternative : 
```cs
app.MapControllerRoute(
    name: "productRoute",
    pattern: "products/{action=List}/{id?}",
    defaults: new { controller = "Product" }
);
```
- Here No `controller` mention so in `defaults` mention the controller.
- `name` it just label