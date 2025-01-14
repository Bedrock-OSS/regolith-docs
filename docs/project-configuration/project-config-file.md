(project-config-file)=
# Project Config File

The configuration of Regolith project is stored inside of `config.json`, at the top level of your Regolith project. This file will be created when you run `regolith init`.

## Project Config Standard

Regolith follows the [Project Config Standard](https://github.com/Bedrock-OSS/project-config-standard). This config is a shared format, used by programs that interact with Minecraft projects, such as ["bridge."](https://editor.bridge-core.app/).

## Regolith Configuration

Regolith builds on this standard with the addition of the `regolith` namespace, which is where all regolith-specific information is stored.

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
- `name`- The name of the project. Regolith uses it to determine the names of the exported packs in some cases. See {ref}`Export Targets<export-targets>` for more information.
- `author`- The author of the project.
- `packs`- The location of the behavior and resource packs.

### Regolith Fields
Everything inside the `regolith` field contains Regolith-specific information.

#### formatVersion
The version of the Regolith configuration format. This is used to determine how Regolith should read the configuration file. Usually, you don't have to worry about this field, Regolith will create it for you when you initialize a project. You can read more about it on the {ref}`format versions page<format-versions>`.

(project-config-data-path)=
#### dataPath
The path to the folder where Regolith will store the data folders of the filters. It's like an extension to `behaviorPack` and `resourcePack` folders, feeding data to your project, but specifically for the Regolith filters.

(filter-definitions)=
#### filterDefinitions
Filter definitions field contains a list of the filters used in the project. Every time you run the `regolith install` command, Regolith will add a new filter to this list with its version and URL, so the field is mostly managed by Regolith.

The only time you should manually edit this field is when you want create a {ref}`local filter<local-filters>`.

The syntax of the `filterDefinitions` field is as follows:
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
    },
}
```
In this example `name_ninja` is a filter downloaded from the internet with {ref}`pinned version<filter-versioning>` 1.2.4, and the `local_filter` is a Python filter that is stored locally.

```{note}
The `venvSlot` property used in the example only make sense in the context of Python filters and very rarely needs to be specified. It is unique in a way that you can specify it in the remote filter definition, and it will be copied to the filter definitions defined in the {ref}`filter.json<online-filter-definition>` file. You can read more about it in the {ref}`venv handling<venv-handling>` section of the Python filters page.
```

The syntax used for the local filters is different basedon the filter kind. You can read more about it in the {ref}`filter definition page<filter-definition>`.

#### profiles
Profiles are sequences of filters that you can run with the `regolith run` command. You can read more about them in the {ref}`profiles page<profiles>`.
