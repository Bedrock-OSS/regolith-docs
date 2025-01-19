(filter-definition)=
# Filter Definition
A filter definition is a JSON object that specifies a reference to a script, executable, or command. These definitions are used in two places:
1. The `filterDefinitions` property in the {ref}`config.json<project-config-file>` file for local filters.
2. The `filters` property in the `filter.json` file for online filters.

While the specific syntax varies by filter type (detailed in their respective sections), all filters must include two key properties:
- **`runWith`** : Specifies the type of filter.
- **Path Property** : Defines the path to the script or executable.

Regolith currently supports the following filter kinds:
- {ref}`.NET<dotnet-filters>`
- {ref}`Deno<deno-filters>`
- {ref}`Executable<executable-filters>`
- {ref}`Java<java-filters>`
- {ref}`Nim<nim-filters>`
- {ref}`NodeJS<node-filters>`
- {ref}`Python<python-filters>`
- {ref}`Shell<shell-filters>`

(local-filter-definition)=
## Local Filter Definition (config.json)
Defining a filter in the `filterDefinitions` property of the {ref}`config.json<project-config-file>` file creates a local filter. The `filterDefinitions` property is a dictionary where:
- The **key**  is the filter's name.
- The **value**  is the filter definition.
The filter name is then referenced in the `filters` property of the same file.

Example:
```json
"filterDefinitions": {
    "my_local_filter": {
        "runWith": "python",
        "script": "filters/my_local_filter/main.py"
    }
}
```
In this example, a local filter named `my_local_filter` runs a Python script located at `filters/my_local_filter/main.py`. Different filter types require specific properties - refer to the documentation for each filter type for more details.

(online-filter-definition)=
## Online Filter Definition (filter.json)
The {ref}`online filters<online-filters>` keep their filter definitions in the `filters` property of their filter.json file. The `filters` list in the filter.json is kind of like a mix of `filterDefinitions` and `filters` from config.json. They contain the definition part of the local filter (with `runWith` proeprty and propertis specific to the filter type) and {ref}`the properties from filters property in config.json<project-config-referencing-filters>`.

Online filters, can't reference other online filters, and profiles.
