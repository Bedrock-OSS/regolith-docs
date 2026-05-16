(user-configuration)=
# User Configuration
The user configuration file is stored in the Regolith app data folder. On Windows, it is located at `%localappdata%\regolith\user_config.json`. On other systems, refer to the Golang documentation for the [os.UserCacheDir](https://pkg.go.dev/os#UserCacheDir) function to find the path it returns that corresponds to the `%localappdata%` on Windows.

The `user_config.json` file stores user preferences for Regolith.

## User Configuration Properties
You can examine the user configuration either by using the {ref}`regolith config<regolith-config-command>` command or by opening the `user_config.json` file in a text editor. Using the `regolith config` command with the `--full` flag will display all properties, including default values (which aren't defined in the file). Below are the properties you may find in the user configuration file.

(use-project-app-data-storage)=
### use_project_app_data_storage: bool
**Default** : `false`

If set to `true`, Regolith will store its project cache (filters, dependencies, etc.) in the {ref}`project-cache<project-cache>` folder, instead of the `.regolith` subfolder located within the project directory.

### username: string
**Default** : `"Your name"`

The user's name, which will be used in the `author` field of the {ref}`config.json<project-config-file>` file when creating a new project.

### resolvers: list[string]
**Default** : `["github.com/Bedrock-OSS/regolith-filter-resolver/resolver.json"]`

A list of {ref}`resolvers<filter-resolvers>` used to resolve filter names to URLs when running the {ref}`regolith install<installing-filters>` command. The default resolver URL is always added at the end of the list.

Note: The "URLs" in the resolvers list are not actual URLs. They consist of two parts, separated by a `/`. The first part is a repository URL (e.g., a GitHub repository), and the second part is the path to the resolver file within the repository. For example, the default resolver is stored in the `github.com/Bedrock-OSS/regolith-filter-resolver` repository at the `resolver.json` file, but `github.com/Bedrock-OSS/regolith-filter-resolver/resolver.json` is not a valid URL.

### resolver_cache_update_cooldown: string
**Default** : `"5m"`

The cooldown duration between updates to the {ref}`resolver repositories<resolver-cache>`. This duration is specified in [Go duration format](https://pkg.go.dev/time#ParseDuration). If you run `regolith install` multiple times within a short period, the resolver cache will only update after the cooldown period has passed.

### filter_cache_update_cooldown: string
**Default** : `"5m"`

The cooldown duration between updates to the {ref}`filter repositories<filter-cache>`. This is also specified in [Go duration format](https://pkg.go.dev/time#ParseDuration) . If you run `regolith install` multiple times quickly, the filter cache will only update after the cooldown period has elapsed.

(tmp-dir-user-config)=
### tmp_dir: string
**Default** : `""`

Specifies the directory where Regolith creates its temporary files for running filters. When not set (or empty), Regolith uses the `.regolith/tmp` folder inside the project directory.

Example:
```
regolith config tmp_dir "R:/"
```

This setting can be used to achieve a significant speed up in filter execution when combined with a RAM drive. This is especially beneficial on the project that heavily rely on reading and writing files in the temporary directory during filter execution, moving it to RAM eliminates disk I/O bottlenecks.

On Windows, you need third-party software (such as ImDisk) to create a RAM drive. On Linux, you can simply leverage `tmpfs`.

```{warning}
Regolith always creates a subfolder inside the specified directory. This prevents accidental file deletion. This is needed because Regolith treats the contents of its working directory as safe to delete. The name of the subfolder is an MD5 hash of the project's root directory path. This prevents collisions when running multiple Regolith instances at the same time.
```


(node-runner-override)=
### node_runner_override: map[string]string
**Default** : `{}`

Allows you to override the runtime used to run NodeJS filters, redirecting them to use Bun or Deno instead. Using Deno or Bun can be faster than NodeJS in some cases.

The map keys are filter IDs (or `*` for a default override) and the values are the runtime to use (`nodejs`, `bun`, or `deno`).

- Setting a key of `*` overrides the runner for all NodeJS filters unless a more specific override exists.
- Setting a key matching a filter ID overrides the runner for that specific filter only.

Example:
```
regolith config node_runner_override "*" bun
regolith config node_runner_override "my_filter" deno
```

This would run all NodeJS filters with Bun, except `my_filter` which would use Deno.

```{warning}
The `*` is a special key. You **can't** use star-based patterns like `some_prefix_*` in configuration to match multiple filters at once. These kind of names would be interpreted as literal keys.
```

### bun_runner: string
**Default** : `null`

Specifies the path to the Bun executable. When not set, Regolith looks for `bun` on the system PATH.

Example:
```
regolith config bun_runner "C:/Programs/bun/bun.exe"
```

### deno_runner: string
**Default** : `null`

Specifies the path to the Deno executable. When not set, Regolith looks for `deno` on the system PATH.

### dotnet_runner: string
**Default** : `null`

Specifies the path to the .NET executable. When not set, Regolith looks for `dotnet` on the system PATH.

### java_runner: string
**Default** : `null`

Specifies the path to the Java executable. When not set, Regolith looks for `java` on the system PATH.

### nim_runner: string
**Default** : `null`

Specifies the path to the Nim executable. When not set, Regolith looks for `nim` on the system PATH.

### nimble_runner: string
**Default** : `null`

Specifies the path to the Nimble executable (used for installing Nim package dependencies). When not set, Regolith looks for `nimble` on the system PATH.

### node_runner: string
**Default** : `null`

Specifies the path to the Node executable. When not set, Regolith looks for `node` on the system PATH.

### npm_runner: string
**Default** : `null`

Specifies the path to the npm executable (used for installing Node package dependencies). When not set, Regolith looks for `npm` on the system PATH.

### python_runner: string
**Default** : `null`

Specifies the path to the Python executable. When not set, Regolith tries the platform-specific executable names (e.g., `python3`, `python`). Regolith uses `python -m pip` to install Python dependencies rather than calling `pip` directly, so unlike some of the other runtimes that use a different executable for running and installation it doesn't need a separate `pip_runner` setting.

Example:
```
regolith config python_runner "C:/Programs/pypy3.11-v7.3.21-win64/pypy.exe"
```

(regolith-config-command)=
## Regolith Config Command
The `regolith config` command is used to manage the user configuration of Regolith. It allows you to access and modify the configuration stored in the `user_config.json` file.

The behavior of this command changes depending on the flags and the number of arguments provided. The following cheat sheet outlines the possible flag and argument combinations and their effects:

- `regolith config` - Prints all properties defined in the user configuration file.
- `regolith config --full` - Prints all properties, including default values for properties that are unspecified.
- `regolith config <setting>` - Prints the value of the specified property.
- `regolith config <setting> <value>` - Sets the value of the specified property.
- `regolith config <setting> --delete` - Deletes the specified property.
- `regolith config <setting> <value> --append` - Appends a value to a list property.
- `regolith config <setting> <value> --index <index>` - Replaces an item in a list property at the specified index.
- `regolith config <setting> --index <index> --delete` - Deletes an item in a list property at the specified index.
- `regolith config <setting> <key> <value>` - Sets a value in a map property at the specified key.
- `regolith config <setting> <key> --delete` - Deletes an entry from a map property at the specified key.

Commands that print text can include the `--full` flag to display the configuration along with default values (if they are not defined in the configuration file). Without this flag, unspecified properties will be shown as null or an empty list.

## User Configuration File
The `user_config.json` file is a regular JSON file with no nesting. While you can edit this file manually, it is not required since all modifications can be done using the `regolith config` command.

Here is an example of a `user_config.json` file:
```json
{
	"use_project_app_data_storage": false,
	"username": "Bedrock-OSS",
	"resolvers": [
		"github.com/Bedrock-OSS/regolith-filter-resolver/resolver.json"
	],
	"tmp_dir": "R:/",
	"node_runner_override": {
		"*": "bun"
	},
	"python_runner": "C:/Programs/pypy3.11-v7.3.21-win64/pypy.exe"
}
```
