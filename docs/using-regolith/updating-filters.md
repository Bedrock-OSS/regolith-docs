# Updating Filers

TODO

## Updating your Filters

If you want to update the version of the filter used in your project, you can use the `regolith install` command again. By default, the `install` command is not allowed to update existing filters, but you can use the `--update` or `--force` flag to change this behavior. The flag must be used after the `install` arguments.

```
regolith install name_ninja --update
```

Alternatively, you can modify the `version` field in `config.json` and run `regolith install-all`. Regolith install-all is useful for working in a team, when other team members may have to update or add filters to the project.

If you want to update all filters in your project, you can use the `--update` flag with the `install-all` command.

```
regolith install-all --update
```