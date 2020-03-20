


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

    endpoints.MapControllerRoute(
        name: "default",
        pattern: "{controller=Home}/{action=Index}/{id?}");
});
```

## Identity
```
dotnet user-secrets init 
dotnet user-secrets set "<provider>:ClientId" "passowrd_here"
```

### Useful links 

- [MS Docs](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/identity-custom-storage-providers?view=aspnetcore-3.1)