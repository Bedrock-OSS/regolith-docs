(installing-filters)=
# Installing Filters

To start using a filter, you need to do four things:

 1. Ensure you can run the filter
 2. Install the filter
 3. Add the filter to the profile which you would like to use it.
 4. Run your profile, to test it out!

## Filter Dependencies

Filters are written in [programming languages](https://www.wikiwand.com/en/Programming_language). These languages may not be installed on your computer by default. Before installing a filter, you should ensure you have the proper programming language installed. The "Filter Types" documentation has detailed installation instructions for every regolith-supported language!

For example, if the filter relies on Python, you can find installation instructions {ref}`here<python-filters>`.

## Installing a Filter

```{warning}
The `install` command relies on `git`. You can read more about Git {ref}`here<git-dependency>`.
```

Regolith contains a powerful installation command, downloads a filter from GitHub, and installs any required libraries for you. In general, the format is like this: `regolith install <filter_identifier>`.

The value of `filter_identifier` will depend on the URL where the filter is hosted. Filters listed on the {ref}`resolvers<filter-resolvers>` in your {ref}`user configuration<user-configuration>` can be installed directly, just with their name. By default Regolith uses the resolver hosted on [Bedrock-OSS/regolith-filter-resolver](https://github.com/Bedrock-OSS/regolith-filter-resolver/blob/main/resolver.json) repository.


For example, to install the `name_ninja` filter (which is one of the filters created by Bedrock-OSS), you would run:
```text
regolith install name_ninja
```

If the filter is not listed on the resolver repository, you need to use the following format:
`github.com/<user>/<repository>/<folder>`.

For example, to install `name_ninja` using the full format, you would run:
```text
regolith install github.com/Bedrock-OSS/regolith-filters/name_ninja
```

The install command accepts multiple arguments, so you can install quickly install multiple fliters by running `regolith install <filter1> <filter2>...`, for example:
```text
regolith install name_ninja texture_list
```

The `install` command also supports installing specific versions of the filters. You can read more about in the {ref}`Filter Versioning<filter-versioning>` page. By default Regolith installs the most recent release of the filter.

## Adding Filter to Profile

After installing, the filter will appear inside `filterDefinitions` of `config.json`. You can now add this filter to a profile like this:

```json
"default": {
  "export": {
    "readOnly": false,
    "target": "development",
    "build": "standard"
  },
  "filters": [
    {
      "filter": "name_ninja", // The name of the filter from filterDefinitions
    }
  ]
}
```

If the filter doesn't need any {ref}`additional configuration<project-config-filters-properties>` you can append it to the end of the list of the filters of the profile by using the `--profile` flag. For example:
```text
regolith install name_ninja --profile=default
```
This command would append the filter to the filters list of the default profile.

## Install All

Regolith is intended to be used with git version control, and by default the {ref}`.regolith<project-cache>` folder is ignored. That means that when you collaborate on a project, or simply re-clone your existing projects, you will need an easy way to download all the filters again!

You may use the command `regolith install-all`, which will check `config.json`, and install every filter in the `filterDefinitions`.


## Cached Results of Regolith Install

When you install multiple filters in a quick succession, it doesn't make much sense to update the filter and resolver respositories {ref}`cached on your computer<regolith-cache>`. The install command checks the time of the last cache update and skips its update, when it's recent enough.

In some situations, you may want to skip the waiting time and force the cache update. The install command, has two flags that you can use to force the cache update during the installation:

- `--force-filter-refresh` - forces the update of the {ref}`filter cache<filter-cache>`, even if the filter repository was downloaded recently.
- `--force-resolver-refresh` - forces the update of the {ref}`resolver cache<resolver-cache>` even if the resolver repository was downloaded recently. This flag is not available for the install-all command, because install-all doesn't use the resolvers, it relies on the URLs provided directly in the {ref}`config.json<project-config-file>` file.

You can change the default cooldown times for downloading in your {ref}`user configuration<user-configuration>`.

If you want to update the filter resolvers, without installing any filters, you can use the following command:
```text
regolith update-resolvers
```