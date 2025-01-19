(dotnet-filters)=
# .NET Filters

.NET filters run compiled .NET programs as filters, using the `dotnet` command.

## Installing .NET

Before you can run .NET filters, you will need to install [.NET Runtime](https://dotnet.microsoft.com/download).

## .NET Filter Definition

The the structure of the .NET filter definition is described below. You can read how to use it in the {ref}`Filter Definition<filter-definition>` section.

```json
{
  "runWith": "dotnet",
  "path": "./filters/example.dll"
}
```

- `runWith` - always set to `dotnet`, marks this filter as a .NET filter.
- `path` - path to the `.dll` file that contains the compiled .NET program to run.
