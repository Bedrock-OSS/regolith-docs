(user-configuration)=
# User Configuration

User configuration file is stored in the Regolith app data folder. On Windows, it's `%localappdata%\regolith\user_config.json`. On other systems, please refer to the Golang documentation of the [os.UserCacheDir](https://pkg.go.dev/os#UserCacheDir) function to find the path it returns that corresponds to the `%localappdata%` on Windows.

The `user_config.json` file is used to store the user preferences for Regolith.

## User Configuration Properties

User configuration can be examined using the {ref}`regolith config<regolith-config-command>` command or by opening the `user_config.json` file in a text editor. The `regolith config` command with `--full` flag will show all properties, including the default values (which aren't defined in the file). This section describes the properties that can be found in the user configuration file.

(use-project-app-data-storage)=
### use_project_app_data_storage: bool

Default: `false`

If set to `true`, the Regolith projects will store their cache (filters, their dependencies, etc.) in the {ref}`project-cache<project-cache>` folder, instead of `.regolith` subfolder stored in the project files.

### username: string

Default: `"Your name"`

The name of the user, which will be used in the `author` field of the {ref}`config.json<project-config-file>` file when creating a new project.

### resolvers: list[string]

Default: `["github.com/Bedrock-OSS/regolith-filter-resolver/resolver.json"]`

A list of {ref}`resolvers<filter-resolvers>`, used to resolve filter names to URLs when using the {ref}`regolith install<installing-filters>` command. The default URL is always added at the end of the list.

Note that the "URLs" used by the resolvers are not actual URLs. They have two parts, separated by `/`. The first part is an URL to a repository on GitHub, and the second part is a path to the resolver file relative to the root of the repository. For example, the default resolver is on the `github.com/Bedrock-OSS/regolith-filter-resolver` repository, in the `resolver.json` file, but `github.com/Bedrock-OSS/regolith-filter-resolver/resolver.json` is not a valid URL.

### resolver_cache_update_cooldown: string

Default: `"5m"`

The cooldown between cache updates for the {ref}`resolver repositories<resolver-cache>`. The cooldown is specified in the [Go duration format](https://pkg.go.dev/time#ParseDuration). If you're running `regolith install` multiple times in a short period, the resolver cache will not be updated every time, but only after the cooldown period.

### filter_cache_update_cooldown: string

Default: `"5m"`

The cooldown between cache updates for the {ref}`filter repositories<filter-cache>`. The cooldown is specified in the [Go duration format](https://pkg.go.dev/time#ParseDuration). If you're running `regolith install` multiple times in a short period, the filter cache will not be updated every time, but only after the cooldown period.

(regolith-config-command)=
## Regolith Config Command

The `regolith config` command is used to manage the user configuration of Regolith. It can access and modify the user configuration file. The data is stored in the application data folder in the `user_config.json` file.

The behavior of the command changes based on the used flags and the number of provided arguments. The cheetsheet below shows the possible combinations of flags and arguments and what they do:

- `regolith config` - Print all properties defined in the user configuration file.
- `regolith config --full` - Print all properties including the default values of the unspecified properties.
- `regolith config <key>` - Print specified property.
- `regolith config <key> <value>` - Set property value.
- `regolith config <key> --delete` - Delete a property.
- `regolith config <key> <value> --append` - append to a list proeprty.
- `regolith config <key> <value> --index <index>` - Replace item in a list property.
- `regolith config <key> --index <index> --delete` - Delete item in a list property.

The commands that print text can take the `--full` flag to print configuration with the default values included (if they're not defined in the config file). Without the flag, the undefined properties will be printed as null or empty list.

## User Configuration File

The `user_config.json` file is just a regular JSON file without any nesting. You can edit it manually if you want to but you don't have to because everything can be done with the `regolith config` command.

Example `user_config.json` file:
```json
{
	"use_project_app_data_storage": false,
	"username": "Bedrock-OSS",
	"resolvers": [
		"github.com/Bedrock-OSS/regolith-filter-resolver/resolver.json"
	]
}
```
