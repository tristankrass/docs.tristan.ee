# Distributed systems


## Generating apis

Updating database and running mingrations
```csharp
dotnet ef migrations add Initial --project DAL --startup-project WebApp
dotnet ef database update --project DAL --startup-project WebApp

dotnet ef database drop --project DAL --startup-project WebApp
```

Generating views and controllers
```shell
dotnet aspnet-codegenerator controller -name PersonsController -actions -m Person -dc ApplicationDbContext -outDir Controllers --useDefaultLayout --useAsyncActions --referenceScriptLibraries -f
```

Generating Razor pages

```
dotnet aspnet-codegenerator razorpage -m TodoTask -dc AppDbContext -udl -outDir Pages/TodoTasks --referenceScriptLibraries -f
```



### Bash script for generating dotnet sln with multiple projects inside it.

`Directory.Build.props.`
```xml
<Project>
    <PropertyGroup>
        <LangVersion>latest</LangVersion>
        <Nullable>enable</Nullable>
    </PropertyGroup>
</Project>
```

```bash
#!/bin/bash
echo name your solution
read solution
#echo which template would you like(mvc, webapp, razor, console, page, webapi)
#read typofapp
dotenet new sln --output ~/Projects/$solution
cd ~/Projects/$solution
dotnet new classlib --framework netstandard2.1 --output Domain
dotnet new classlib --framework netstandard2.1 --output DAL.App.EF
dotnet new classlib --framework netstandard2.1 --output DTO
dotnet new classlib --framework netstandard2.1 --output Contracts.DAL.Base
dotnet sln add Domain
dotnet sln add DAL.App.EF
dotnet sln add DTO
dotnet sln add Contracts.DAL.Base
#dotnet new $typofapp --framework netcoreapp3.1 --output WebApp
#dotnet sln add WebApp
cd ~/Projects/$solution
```

## Useful links
