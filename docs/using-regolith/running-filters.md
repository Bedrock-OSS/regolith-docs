(running-filters)=
# Running Filters

There are three ways to run Regolith:
- `regolith run`
- `regolith watch`
- `regolith apply-filter`

## Run and Watch Commands
The `run` and `watch` commands are quite similar. Both execute a profile, but there is a key difference: the `watch` command monitors changes in the RP, BP, {ref}`data<data-folder>` folders and optionally additional folders specified in the {ref}`watchPaths<watch-paths>` property of the configuration file, automatically rerunning the profile when changes are detected. In contrast, the `run` command executes the profile only once.The syntax for the `run` and `watch` commands is as follows:

```text
regolith run [profile-name]
```

```text
regolith watch [profile-name]
```

Here, `[profile-name]` refers to the name of the profile defined in your {ref}`config.json<project-config-file>` file that you wish to run. If you don't specify a profile name, the `default` profile will be used.

A single run performs the following steps:
1. Copy your source files into a temporary folder.
2. Run all of the filters specified in the profile.
3. Move the processed files to the target location defined in the profile's "export" property.

Filters work on copies of the RP, BP, and data folders, ensuring that the original files remain untouched. This non-destructive behavior is preserved when using both the `run` and `watch` commands.

```{warning}
Some filters may modify the data folder if they opt into this feature. You can read more about this feature {ref}`here<filter-property-export-data>`. This functionality is useful for filters that need to store data between runs.
```

## Apply-Filter Command
While `regolith run` and `regolith watch` are safe operations (as they generally don't modify project files), the `regolith apply-filter` command permanently applies the results of running a filter to your project.

You can use the command as follows:

```text
regolith apply-filter <filter-name> [args...]
```
Here, `<filter-name>` refers to the name of the filter you want to apply, and `[args...]` are any arguments you wish to pass to the filter.
