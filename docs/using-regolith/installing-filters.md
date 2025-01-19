(installing-filters)=
# Installing Filters
To begin using a filter in Regolith, follow these four steps:

1. Ensure that you can run the filter.
2. Install the filter.
3. Add the filter to the desired profile.
4. Run your profile to test the filter.

## Filter Dependencies
Filters are typically written in specific programming languages, and these languages may not be installed on your computer by default. Before installing a filter, ensure you have the required programming language(s) installed. Detailed installation instructions for every Regolith-supported language can be found in the "Filter Types" documentation.

For instance, if a filter depends on Python, you can find the installation instructions {ref}`here<python-filters>`.

(install-command)=
## Install Command
```{warning}
The `install` command requires `git`. You can read more about Git {ref}`here<git-dependency>`.
```

Regolith provides a powerful `install` command that downloads filters from Git repositories and installs any necessary libraries. The general format is:
```text
regolith install <filter_identifier>
```

The `filter_identifier` depends on where the filter is hosted. Filters listed in the {ref}`resolvers<filter-resolvers>` of your {ref}`user configuration<user-configuration>` can be installed directly by name. By default, Regolith uses the resolver hosted on the [Bedrock-OSS/regolith-filter-resolver](https://github.com/Bedrock-OSS/regolith-filter-resolver/blob/main/resolver.json) repository.

For example, to install the `name_ninja` filter (a Bedrock-OSS filter), run:
```text
regolith install name_ninja
```

If the filter is not listed in the resolver repository, you need to use the following format:
```text
regolith install github.com/<user>/<repository>/<folder>
```

Or, for non-GitHub hosted filters:
```text
regolith install <repository-url>/<folder>
```

For example, to install `name_ninja` using the full format:
```text
regolith install github.com/Bedrock-OSS/regolith-filters/name_ninja
```

You can install multiple filters at once by passing multiple arguments:
```text
regolith install name_ninja texture_list
```

The `install` command also supports installing specific versions of filters. For more details, refer to the {ref}`Filter Versioning<filter-versioning>` page. By default, Regolith installs the latest release of each filter.

## Adding Filter to Profile
Once the filter is installed, it will appear in the `filterDefinitions` section of `config.json`. You can now add it to a profile, like this:

```json
"default": {
  "export": {
    "readOnly": false,
    "target": "development",
    "build": "standard"
  },
  "filters": [
    {
      "filter": "name_ninja" // The name of the filter from filterDefinitions
    }
  ]
}
```
If the filter doesn't need any {ref}`additional configuration<project-config-filters-properties>` you can append it to the end of the list of the filters of the profile by using the `--profile` flag. For example:
```text
regolith install name_ninja --profile=default
```
This command will automatically add the filter to the filter list of the `default` profile.

## Install All Command
Regolith is designed to be used with Git version control. By default, the {ref}`.regolith<project-cache>` folder is ignored. This means that when collaborating on a project or re-cloning existing ones, you'll need a quick way to re-download all the filters.

You can use the `regolith install-all` command, which checks your `config.json` file and installs every filter listed in the `filterDefinitions`.

## Cached Results of Regolith Install
When installing multiple filters in quick succession, Regolith avoids unnecessary updates to the filter and resolver repositories that are {ref}`cached on your computer<regolith-cache>`. It checks the timestamp of the last cache update and skips refreshing the cache if it's recent enough.

In some situations, you might want to skip the cache wait time and force an update. The `install` command has two flags that can force a cache update:

- `--force-filter-refresh`: Forces the update of the {ref}`filter cache<filter-cache>`, even if the filter repository was downloaded recently.
- `--force-resolver-refresh`: Forces the update of the {ref}`resolver cache<resolver-cache>`, even if the resolver repository was downloaded recently. Note: This flag is not available for the `install-all` command because `install-all` doesn't use resolvers; it depends on the URLs provided directly in the {ref}`config.json<project-config-file>`.

You can adjust the default cooldown times for downloading filters in your {ref}`user configuration<user-configuration>`.

If you want to update the filter resolvers, without installing any filters, you can use the following command:
```text
regolith update-resolvers
```
