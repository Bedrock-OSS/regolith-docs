(filter-definition)=
# Filter Definition

Filter definition is a JSON object that defines a single reference to a script/executable, or a command to run. The filter defnitions are used in two places - in the config.json file in `filterDefinitions` property, and in the filter.json file in the `filters` property.

The syntax of the of every kind of filter is different and explained in their respective sections, but in general all filters need to have two properties - `runWith` to specify the filter kind, and a property that specifies the path to the script/executable.

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
If you put a filter definition in the {ref}`filterDefinitions<filter-definitions>` property of the {ref}`config.json<project-config-file>` file, you create a local filter. The `filterDefinitions` property is a dictionary where the key is the name of the filter, and the value is the filter definition. The name of the filter is later used in the `filters` property of the same file to reference the filter.

Example:
```json
"filterDefinitions": {
    "my_local_filter": {
        "runWith": "python",
        "script": "filters/my_local_filter/main.py"
    }
}
```
This snippet shows how to define a local filter named `my_local_filter` that runs a Python script located in the `filters/local_filter/main.py` file. Different kinds of filters have different properties, please refer to the specific filter type in the Filters documentation section for more information.

(online-filter-definition)=
## Online Filter Definition (filter.json)

The {ref}`online filters<online-filters>` keep their filter definitions in the `filters` property of their filter.json file. The `filters` list in the filter.json is kind of like a mix of `filterDefinitions` and `filters` from config.json. They contain the definition part of the local filter (with `runWith` proeprty and propertis specific to the filter type) and {ref}`the properties from filters property in config.json<project-config-referencing-filters>`.

Online filters, can't reference other online filters, and they can't reference profiles.
