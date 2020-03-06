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

> `Directory.Build.props.` - Enable the latest language features.
```xml
<Project>
    <PropertyGroup>
        <LangVersion>latest</LangVersion>
        <Nullable>enable</Nullable>
    </PropertyGroup>
</Project>
```

## Useful links
