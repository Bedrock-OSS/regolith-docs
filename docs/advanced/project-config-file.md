(project-config-file)=
# Project Config File

The configuration of Regolith project is stored inside of `config.json`, at the top level of your Regolith project. This file will be created when you run `regolith init`.

## Project Config Standard

Regolith follows the [Project Config Standard](https://github.com/Bedrock-OSS/project-config-standard). This config is a shared format, used by programs that interact with Minecraft projects, such as ["bridge."](https://editor.bridge-core.app/).

## Regolith Configuration

Regolith builds on this standard with the addition of the `regolith` namespace, which is where all regolith-specific information is stored.

```{warning}
This page only shows an example configuration. There are other documentation pages to fully explain concepts such as `filters` and `profiles`.
```

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
The version of the Regolith configuration format. This is used to determine how Regolith should read the configuration file. Usually, you don't have to worry about this field, Regolith will create it for you when you initialize a project.

```{warning}
The `formatVersion` field was introduced quite late in the development of Regolith. The format version changes when the format of the configuration file changes in a way that breaks the backward compatibility. The format versions use the same version number as the version of Regolith that introduce them. Not all versions of Regolith add new format version. The lowest possible value and the default (if not specified) is `1.2.0`.
```

Below is a list of available format versions and the changes they introduced:

- `1.2.0` - The first available `formatVersion'. This is the default if the field is not specified.
- `1.4.0` - This version changed the way the `export` field works. You can read about the current implementation of the export target in {ref}`it's own page<export-targets>`. Unfortunately, the `1.4.0` format change was implemented before we had versioned documentation, so the only way to read about it now is to look at the [source of the old version of the documentation](https://github.com/Bedrock-OSS/regolith/blob/1.2.0/docs/docs/guide/export-targets.md).

#### dataPath
The path to the folder where Regolith will store the data folders of the filters. It's like an extension to `behaviorPack` and `resourcePack` folders, feeding data to your project, but specifically for the Regolith filters.

(filter-definitions)=
#### filterDefinitions
Filter definitions is mostly managed by Regolith itself. It contains a list of the filters used in the project. Every time you run the `regolith install` command, Regolith will add a new filter to this list with its version and URL.

The only time you should manually edit this field is when you want create a {ref}`local filter<local-filters>`.

#### profiles
Profiles are sequences of filters that you can run with the `regolith run` command. You can read more about them in the {ref}`profiles page<profiles>`.
