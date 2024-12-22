# Updating Filers

By default, when you try to install a filter that is already on the {ref}`filter definitions<filter-definitions>` list, Regolith won't let you do that. If you want to reinstall or update the filter, you need to use a flag for that.

## Updating With the "install" Command

If you want to update the version of the filter used in your project, you can use the `regolith install` command with the `--update` flag. For example:

```text
regolith install name_ninja --update
```
This command updates the name_ninja to the latest version available. It's exactly the same as running `regolith install name_ninja` before the filter is insatlled for the same time.

The `--force` and `--update` flags in the `install` are **aliases**; they do the same thing.

## Updating With the "install-all" Command

Alternatively, you can modify the `version` field in `config.json` and run `regolith install-all` (without any flags).

OR, if you want to update all filters in your project to their newest available versions, you can use:
```text
regolith install-all --update
```

Unlinke in the `install` command, `--update` and `--force` flags in the `install-all` command are **different**.

- The `--update` flag in `install-all` is the same as running the `install` command for each filter listed in the `filterDefinitions` with the `--update` flag (it changes the versions of the filters).
- The `--force` flag in `install-all` reinstalls all of the filters without changing their versions.
