# Filter Versioning

TODO

Filters in Regolith are optionally versioned with a [semantic version](https://semver.org/). As filters get updated, new versions will be released, and you can optionally update.

```{warning}
If you don't specify a version, the `install` command will pick a sensible default. First, it will search for the latest release. If that doesn't exist (such as a filter that has no versions), it will select the latest commit in the repository. In both cases, the installed version will be `pinned`.
```

## Installing a Specific Version

When installing, you can optionally include a version key after two  equals signs (`==`):

 - ⭐ Version: `regolith install name_ninja==1.2.8`
 - Unpinned Head: `regolith install name_ninja==HEAD`
 - Unpinned Latest: `regolith install name_ninja==latest`
 - SHA: `regolith install name_ninja==adf506df267d10189b6edcdfeec6c560247b823f`

## Pinned Versions

In your `config.json`, every filter will include a `version` field, which specifies which version of the filter to use. By default, this version will be `pinned`, meaning that it won't be updated, even if new versions release. This provides you safety, and ensures that your projects will continue to operate without interruption even if filters release breaking changes.

Optionally, you may mark filters as `unpinned`, which signifies that your project wants the latest version of the filter, no questions asked. There are two available `unpinned` versions:
 - `latest` points to the latest released version tag.
 - `HEAD` points to the latest commit of the repository, regardless of release tags.

## Updating filter cache

Regolith caches the filter repository when you install online filters. To avoid unnecessary frequent updates, Regolith skips them for installations that occur less than 5 minutes after the last update.
However, if you need to update the cache immediately, you can use the `--force-filter-update` flag while installing a filter.

```bash
regolith install name_ninja --force-filter-update
# OR
regolith install-all --force-filter-update
```