(project-config-file)=
# Project Config File
The configuration for a Regolith project is stored in the `config.json` file located at the root level of your project. This file is automatically created when you run the `regolith init` command.

## Project Config Standard
Regolith adheres to the [Project Config Standard](https://github.com/Bedrock-OSS/project-config-standard). This format is shared among various tools that interact with Minecraft projects, such as ["bridge."](https://editor.bridge-core.app/).

## Regolith Configuration
Regolith extends the standard with the addition of a `regolith` namespace, where all Regolith-specific information is defined.

Example configuration file:
```json
{
    "name": "Project Name",
    "author": "Author Name",
    "packs": {
        "behaviorPack": "./packs/BP",
        "resourcePack": "./packs/RP"
    },
    "regolith": {
        "formatVersion": "1.4.0",
        "dataPath": "./packs/data",
        "watchPaths": ["custom_watched_folder"],
        "filterDefinitions": {
            "bump_manifest": {
                "url": "github.com/Bedrock-OSS/regolith-filters",
                "version": "1.0.0"
            },
            "name_ninja": {
                "url": "github.com/Bedrock-OSS/regolith-filters",
                "version": "1.2.4"
            }
        },
        "profiles": {
            "default": {
                "filters": [
                    {
                        "filter": "name_ninja",
                        "settings": {
                            "language": "en_GB.lang"
                        }
                    },
                    {
                        "filter": "bump_manifest",
                        "arguments": ["-regolith"],
                        "disabled": true,
                        "when": "os == 'windows' && arch == 'amd64'"
                    }
                ],
                "export": {
                    "target": "development",
                    "build": "standard",
                    "readOnly": false
                }
            }
        }
    }
}
```

### Project Config Standard Fields
- `name`: The name of the project. Regolith may use this value to name exported packs. For more details, see {ref}`Export Targets<export-targets>`.
- `author`: The author of the project.
- `packs`: Specifies the locations of the behavior and resource packs.

### Regolith Fields
The `regolith` field contains all Regolith-specific configurations.

#### formatVersion
Specifies the version of the Regolith configuration format. This field determines how Regolith interprets the configuration file. Generally, you don't need to modify this field, as Regolith automatically sets it during project initialization. For more details, refer to the {ref}`format versions page<format-versions>`.

(project-config-data-path)=
#### dataPath
Defines the path to the folder where Regolith stores the data used by filters. This folder acts as an extension to the `behaviorPack` and `resourcePack` directories, providing additional data specifically for use with Regolith filters.

(watch-paths)=
#### watchPaths
An optional array of additional paths that Regolith monitors for changes when using the `regolith watch` command. This allows you to include custom folders. Relative paths are relative to the project root.

(filter-definitions)=
#### filterDefinitions
The `filterDefinitions` field lists all filters used in the project. Whenever you run the `regolith install` command, Regolith updates this field by adding new filters along with their versions and URLs.Typically, this field is managed by Regolith, and manual editing is not required unless you need to create a {ref}`local filter<local-filters>`.Here's an example of the `filterDefinitions` syntax:
```json
"filterDefinitions": {
    "name_ninja": {
        "url": "github.com/Bedrock-OSS/regolith-filters",
        "version": "1.2.4",
        "venvSlot": 0
    },
    "local_filter": {
        "runWith": "python",
        "script": "filters/local_filter/main.py"
    }
}
```
In this example:

- `name_ninja` is a filter downloaded from the internet with a {ref}`pinned version<filter-versioning>` of 1.2.4.

- `local_filter` is a Python-based filter stored locally within the project.

```{note}
The `venvSlot` property used in the example only makes sense in the context of Python filters and is rarely required. When specified in a remote filter definition, it is copied into the filter definitions found in the {ref}`filter.json<online-filter-definition>` file. For more details, see the {ref}`venv handling<venv-handling>` section of the Python filters page.
```
The syntax for local filters varies depending on the filter type. Refer to the {ref}`filter definition page<filter-definition>` for more information.


#### profiles
Profiles define sequences of filters to execute using the `regolith run` command. Learn more about profiles on the {ref}`profiles page<profiles>`.
