


### MiddleWare

Simple midldleware demo would be: 
<details>
<summary>Code example</summary>

```csharp
using middleWare;
// Inside Startup.cs
app.UseCustomMiddleWare("/custom");
app.Run(async ctx =>
{ 
    await ctx.Response.WriteAsync("final");
});

// ClassLib for middleware
public class CustomMiddleware
{
    private readonly RequestDelegate _next;
    private readonly string _endpointPath;

    public CustomMiddleware(RequestDelegate next, string path)
    {
        _next = next;
        _endpointPath = path;
    }

    public async Task InvokeAsync(HttpContext ctx)
    {
        if (ctx.Request.Path.Value.StartsWith(_endpointPath))
        {
            await ctx.Response.WriteAsync(ctx.Request.Path.Value + "-------Before---------\n");

        }

        await _next(ctx);

        await ctx.Response.WriteAsync("\n-------After---------\n");

    }
}
// Extension method that gets called from startup.cs
using Microsoft.AspNetCore.Builder;

namespace MiddleWare
{
    public static class CustomMiddleWareExtension
    {
        public static IApplicationBuilder UseCustomMiddleWare(this IApplicationBuilder builder, string path)
        {
            return builder.UseMiddleware<CustomMiddleware>(path);
        }
    }
}
```
</details>

### Routing and Url Parameters

<details>
<summary>routing example</summary>

```csharp
// Inside the Controller method
// param ?id=s123 will get automatically binded to this method
 public string Show(string author, int article)
{
    return "Articles show: " + article + " " + author;
}
// Inside the starup.cs file we can specify what will happen to query params, default is:
app.UseEndpoints(endpoints =>
{
  // we can modify the url for each controller
  endpoints.MapControllerRoute(
                    name: "article",
                    pattern: "articles/show/{author?}/{article}",
                    new {controller = "Articles", action = "Show"}
                );
    // add a control how long the param is
    endpoints.MapControllerRoute(
                    name: "articleStr",
                    pattern: "articles/show/{author?}/{article:alpha:minlength(5)}",
                    new {controller = "Articles", action = "ShowStr"}
                );

    // Catch anything 
    endpoints.MapControllerRoute(
                    name: "default",
                    pattern: "{*paramss}",
                    new {controller = "Articles", action = "CatchAll"}
                );
      
    // Default controller is Home
    endpoints.MapControllerRoute(
        name: "default",
        pattern: "{controller=Home}/{action=Index}/{id?}");
});
```
</details>

### Model Binding
<details>
</details>

Inside the mvc the method that returns View(), they must
have accompanyng view in the view folder named after the controller.
Meaning, if you have a method named `Test()` inside the controller, you must have the `Test.cshtml` inside the view folder.

For methods that have the same signature, but serve the same endpoint, use attribues like `[HttpPost]`

If there is a post and the form is empty then the result is taken from the query string.
Priority is the following:
1. Form value
2. Route value
3. Query params


## Identity

Generating UI for the identity 
```bash
dotnet aspnet-codegenerator identity -dc DAL.App.EF.ApplicationDbContext  -f
```
Inside the `Startup.cs` file we will specify, what our custom identityUser looks like.
```csharp
 services.AddDefaultIdentity<AppUser>(options => options.SignIn.RequireConfirmedAccount = true)
                .AddEntityFrameworkStores<ApplicationDbContext>();

// Inside shared/_LoginPartial, must change the old appuser to new one
@inject SignInManager<AppUser> SignInManager
@inject UserManager<AppUser> UserManager

```



```
dotnet user-secrets init 
dotnet user-secrets set "<provider>:ClientId" "passowrd_here"
```

### Views
Inside the views when we post the forms, the model 
binding automatically tries to create a new Object that is specific to this controller an view. 
example:
```html
<form>
    <input asp-for="Person.FirstName"/>
</form>
```
The input will automatically gets binded to the method inside the controller.
```csharp
person = new Person()
person.FirstName = Request.Form['FirstName'] // gets input from asp-for
```
[BinRequired] && [BindNever] will specify whether or not the specific property on the gets binded or not.
[Bind("PersonId, ....")] Is not a good idea since first it is a magic string and then it can drop out of sync with the actual domain model.

Some cases if we want to revalidate the model, then 
it's possible to call `TryValidateModel(someMode)` again.

For custom validation errors use:
`ModelState.AddModelError("key", "Error message here")`

ModelState.Remove("Key<Person.FirstName>")

#### Customizing views
To add specific _Layout.cshtml that every file in current directory should use as their base. This is done by creating a file `_ViewStart.cshtml` Inside there
```csharp
@{
    // The convention is to name layout files startting with underscore
    Layout = "_customLayout";
}
```
Adding partial
Good for reuse. Most of the views share common code between them.
Create a .cshtml where the code lives and use it inside other cshtml files by calling 
<partial name="name_of_partial"/>


### Areas
When the projects get really big it's benefitial to split the views up. One way to approach is to use
areas. Little containers that each live on their own.

[Area("Admin")]
[Area("Client")]
- Areas
    - Admin
        - Controllers
        - Views
        - Models
    
    - Client
        - Controllers
        - Views
        - Models

Linking inside the same area is not mandator, but outside the area it's done by
adding asp-area property.
```html
<a asp-area="Admin" asp-controller="Home" asp-action="Index">Home</a>
```


#### Tag helpers (Formating)
Asp-format="<formay>"
use to format value
<input asp-for="SomeNumber" asp-format="{0:N4}" /> //For example descimal places

```csharp
app.UseMvc(routes =>
{
    routes.MapRoute(name: "areaRoute",
    template: "{area:exists}/{controller=Home}/{action=Index}"
    );

    routes.MapRoute(
        name: "default",
        template: "{controller=Home}/{action=Index}/{id?}");
    )
}
```

### Useful links 

- [MS Docs](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/identity-custom-storage-providers?view=aspnetcore-3.1)