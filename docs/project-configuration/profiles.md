(profiles)=
# Profiles

A `profile` is a collection of filters, and export information. By default, a Regolith project is initialized with a single profile, called `default`.

You can add additional profiles, as you need them. For example, `default` profile may build a base version of the project, similar to the one you would use to release the project. You can create a `dev` profile that {ref}`runs the default profile<using-profiles-as-filters>` and adds development focused content on top of that or a `build` profile that additionally creates a compressed version of the project for distribution. You can also use different profiles to export to different locations, like for example Minecraft Education Edition and Minecraft Bedrock Edition.

You can run specific profiles using the `regolith run <profile name>` command.


A profile is a JSON object, that you define in the `config.json` file inside the `profiles` object. The code snippet below shows their structure, you can view the structure of an example `config.json` file {ref}`here<project-config-file>`.

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
    ]
  },
  "otherProfile": {
    "export": {
      "target": "local",
    },
    "filters": [
      {
        "profile": "default"
      }
    ]
  }
}
```

The code above defines two profiles, `default` and `otherProfile`. The `default` profile contains two filters, `name_ninja` and `bump_manifest` and the content of the `otherProfile` is omitted for brevity. A profile must contain two fields - `filters` and `export`.

## Export Properties
Export field defines where the files will be exported. It's relatively complex, so it has its own page {ref}`here<export-targets>`.

(project-config-filters-properties)=
## Filters Properties

The filters field is an array of objects, each of which has references to things to run (filters or other profiles).

(using-profiles-as-filters)=
### Referencing Profiles

When the object in the `filters` array contains a `profile` field, its structure is very simple. It only contains the name of the profile to run. The profile must be defined in the `profile` property. 

Using profiles is useful when you want to have a multiple similar filters and you want to avoid writing the same configuration multiple times.

(project-config-referencing-filters)=
### Referencing Filters

When the object in the `filters` array continas a `filter` field, it references a filter defined in {ref}`filterDefinitions<filter-definitions>`. It may also contain additional properties defining how to run the filter and under what conditions.

#### filter: string
Filter is a required filed that references the filter to run. The filter must be defined in the `filterDefinitions` object in the project's `config.json` file.

#### arguments: list
Arguments is an optional field that specify the command-line arguments to pass to the filter when it runs. It's an array of strings that are passed as arguments to the filter. Different filters may use this field differently, so you should refer to the filter's documentation for more information.

#### settings: object
Settings, like arguments, is an optional field that affects the command-line arguments. When it's present, its content is passed to the filter as a JSON string as the first argument. Different filters may use this field differently, so you should refer to the filter's documentation for more information.

#### disabled: bool
The optional `disabled` field is added for convenience. You can set it to `true` to disable a filter without removing it from the profile. This can be useful when you want to temporarily disable a filter without losing the configuration.

(project-config-when-property)=
#### when: string
The optional `when` field is a boolean expression that disables the filter when it's false. The most common use case is to run a filter only on a specific operating system or architecture. You can read more about the syntax and available variables on it's own page {ref}`here<go-simple-eval>`.
