(nim-filters)=
# Nim Filters

Nim filters compile and run Nim programs from their source code. Nim filters are stored as the source code and may have additional dependencies that Regolith will download for you during `regolith install` execution.

## Installing Nim

You can download Nim from the [official website](https://nim-lang.org/install.html). We recommend using the `choosenim` tool (also available on the official website) to install Nim.

## Nim Filter Definition

The structure of the Nim filter definition is described below. You can read how to use it in the {ref}`Filter Definition<filter-definition>` section.

```json
{
  "runWith": "nim",
  "script": "./filters/example.nim",
  "requirements": "./filters"
}
```

- `runWith` - always set to `nim`, marks this filter as a Nim filter.
- `script` - path to the `.nim` or `.nims` file that contains the Nim program to run. Regolith compiles the script during `regolith install` even if the extension is `.nims` (Nim script file).
- `requirements` (optional) - a property that defines the path to the folder with the `.nimble` file. By default, Regolith looks for the `.nimble` file in the same folder as the script.


## Requirements and Dependencies

The dependencies of a Nim filter are defined in a `.nimble` file. You can read more about the `.nimble` file in the Nim documentation. The Nim filters expect the dependencies to be defined in a `.nimble` file in the same directory as the script file unless specified otherwise in the `requirements` property.
