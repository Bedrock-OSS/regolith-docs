(running-filters)=
# Running Filters

There are 3 ways of running Regolith:
- `regolith run`
- `regolith watch`
- `regolith apply-filter`

## Run and Watch Commands

Regolith `run` and `watch` are very similar to each other. They run a profile. The difference is that the `watch` command will watch for changes in the RP, BP and {ref}`data<data-folder>` folders and rerun the profile when they change. The `run` command will run the profile only once.

The syntax for run and watch command is:

```text
regolith run [profile-name]
```

```text
regolith watch [profile-name]
```

Where `[profile-name]` is the name of the profile defined your {ref}`config.json<project-config-file>` file you want to run. The `[profile-name]` is optional. If you don't specify it, the `default` profile will be run.

A single run performs the following steps:
1. Copy your source files into a temporary folder.
2. Run all of the filters of the profile.
3. Move the files to the target location defined in the "export" property of the profile.

Filters work on the copies of RP, BP, and data. Thanks to the use of copies RP, BP and data are not modified making the run and watch non-destructive.

```{warning}
Some of the filters may modify the data folder if the choose to opt-in for this feature. You can read more about this feature {ref}`here<filter-property-export-data>`. This feature is useful for the filters that need to store some data between runs.
```

## Apply-Filter Command

Running Regolith with `regolith run` or `regolith watch` is a safe operation because they generally don't modify the files of the project.

If you want to apply the results of running a filter permanently to you project, you can use the `regolith apply-filter` command.

The command is used like this:
```text
regolith apply-filter <filter-name> [args...]
```
The `filter-name` is the name of one of the filters installed in your project. The `args` is a list of arguments passed to the filter.
