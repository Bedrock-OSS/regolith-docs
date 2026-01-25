(profiles)=
# Profiles
A `profile` is a collection of filters and export information. By default, a Regolith project is initialized with a single profile called `default`.

You can create additional profiles as needed. For example:
- The `default` profile may build a base version of the project, similar to a release-ready version.
- A `dev` profile could {ref}`run the default profile<project-config-referencing-profiles>` and add development-focused content.
- A `build` profile might include additional steps to create a compressed version of the project for distribution.
- Profiles can also target different locations, such as Minecraft Education Edition or Minecraft Bedrock Edition.

You can run specific profiles using the `regolith run <profile name>` command.

A profile is a JSON object defined in the `config.json` file inside the `profiles` object. Below is an example of their structure. For a complete example of a `config.json` file, refer {ref}`here<project-config-file>`.

```json
"profiles": {
  "default": {
    "export": {
      "target": "development",
      "build": "standard",
      "readOnly": false
    },
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
    "preShell": {
      "windows": ["$env:OS_NAME = 'Windows'"],
      "linux": ["export OS_NAME='Linux'"],
      "darwin": ["export OS_NAME='macOS'"]
    },
    "postShell": [
      "echo This will run on every OS",
      "echo You can have multiple commands here"
    ]
  },
  "otherProfile": {
    "export": {
      "target": "local"
    },
    "filters": [
      {
        "profile": "default"
      }
    ]
  }
}
```

The code above defines two profiles:
- `default`: Includes two filters, `name_ninja` and `bump_manifest`.
- `otherProfile`: References the `default` profile.

A profile must contain two fields - `filters` and `export`.

## Export Properties
The `export` field defines where the files will be exported. Since it can be complex, it is covered on its dedicated page {ref}`here<export-targets>`.

(project-config-pre-and-post-shell)=
## preShell and postShell Properties
The optional `preShell` and `postShell` fields allow you to specify shell commands that run before and after the filters, respectively. They accept either a list of commands (to run on all operating systems) or an object with OS-specific commands. They're especially useful for setting {ref}`environment variables<environment-variables>` to be used by the filters.

(project-config-filters-properties)=
## Filters Properties
The `filters` field is an array of objects. Each object references items to run (filters or other profiles).

(project-config-referencing-profiles)=
### Referencing Profiles
If an object in the `filters` array contains a `profile` field, it references another profile. This allows you to reuse and extend existing configurations.

Using profiles is especially helpful when you have multiple similar filters and want to avoid redundant configuration.

```{note}
Some of the properties that you can use for profile references are described below in the {ref}`Common Properties<project-config-common-properties>` section.
```

(project-config-referencing-filters)=
### Referencing Filters
If an object in the `filters` array contains a `filter` field, it references a filter defined in {ref}`filterDefinitions<filter-definitions>`. This object can also include additional properties to customize how the filter runs.

```{note}
Some of the properties that you can use for filter references are described below in the {ref}`Common Properties<project-config-common-properties>` section.

Properties unique to filter references are described below.
```

#### filter: string
This required field specifies the filter to run. The filter must be defined in the `filterDefinitions` object within `config.json`.

#### arguments: list
Arguments is an optional field that specify the command-line arguments to pass to the filter. It's an array of strings that are passed as arguments to the filter. Different filters may use this field differently, so you should refer to their documentation for more information.

#### settings: object
Settings, like arguments, is an optional field that affects the command-line arguments. When it's present, its content is passed to the filter as a JSON string as the first argument. Like `arguments`, its purpose depends on the specific filter.

(project-config-extra-arguments-property)=
#### extraArguments: string
The optional `extraArguments` field defines the behaviour for arguments passed to regolith from `regolith run` or `regolith watch` commands.

This can be one of the following:
- `ignore` (default) - Extra arguments are ignored. Only arguments from the `arguments` field are passed to the filter.
- `override` - Arguments passed into the command replace those provided by the `arguments` field.
- `append` - Extra arguments are added to the end of the arguments list provided by the the `arguments` field.

You can read more about passing extra arguments to filters in the {ref}`Passing Extra Arguments to Filters<passing-extra-arguments-to-filters>` section of the Running Filters page.

(project-config-common-properties)=
### Common Properties
The following properties can be used for both filter and profile references.

#### disabled: bool
An optional field for convenience. Set to `true` to disable a filter temporarily without removing it from the profile.

(project-config-when-property)=
#### when: string
The optional `when` field is a boolean expression that determines whether a filter runs. If the expression evaluates to `false`, the filter is skipped.This field is commonly used to target specific operating systems or architectures. You can learn more about its syntax and available variables {ref}`here<go-simple-eval>`.

(project-config-running-async-filers)=
### Referencing filters to run in parallel
If an object in the `filters` array contains a `asyncFilters` field, it references a list of filter objects (as above) defined in {ref}`filterDefinitions<filter-definitions>` that are ran in parallel.
```json
{
    "filters": [
        {
            "filter": "example1"
        },
        {
            "asyncFilters": [
                {
                    "filter": "example2"
                },
                {
                    "filter": "example3"
                }
            ]
        }
    ]
}
```

```{warning}
When running filters in parallel, the order of execution is not guaranteed. Make sure that the filters do not have dependencies on each other to avoid unexpected behavior.
```
