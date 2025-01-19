# Updating Filters
By default, Regolith prevents you from installing a filter that is already listed in your {ref}`filter definitions<filter-definitions>`. If you want to reinstall or update the filter, you must use specific flags.

## Updating With the "install" Command
To update the version of a filter used in your project, you can use the `regolith install` command with the `--update` flag. For example:
```text
regolith install name_ninja --update
```

This command updates the `name_ninja` filter to the latest version available. It works the same way as running `regolith install name_ninja` before the its first installation.

The `--force` and `--update` flags in the `install` command are **aliases**  and perform the same function.

## Updating With the "install-all" Command
Alternatively, you can modify the `version` field in `config.json` and run `regolith install-all` (without any flags).

Or, if you want to update all filters in your project to their newest available versions, you can use:
```text
regolith install-all --update
```

Unlike in the `install` command, the `--update` and `--force` flags in the `install-all` command have **different meanings** .

- The `--update` flag in `install-all` behaves as if you ran the `install` command for each filter listed in `filterDefinitions` with the `--update` flag. It updates the versions of the filters.
- The `--force` flag in `install-all` reinstalls all of the filters without changing their versions.
