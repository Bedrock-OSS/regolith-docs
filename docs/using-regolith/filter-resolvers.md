# Filter Resolvers

TODO

## Updating resolvers

When using short names for filters, Regolith uses a resolver file from a remote repository to determine the URL of the filter.
By default, this remote repository is cached and only updated after 5 minutes since last update. If you want to update the resolver file immediately, you can use the `regolith update-resolver` command.

Alternatively, you can use the `--force-resolver-update` flag to force the resolvers to update when installing a filter.

```
regolith install name_ninja --force-resolver-update
```
