(filter-versioning)=
# Filter Versioning

Regolith filters are versioned either with versions assigned by its creator using [semantic version](https://semver.org/), or simply by SHA values of the commits on their GitHub repository. When you install a filter, by default Regolith saves the version it installed in the {ref}`config file<project-config-file>`.

## Version Pinning

When installing, you can optionally include a version key after two  equals signs (`==`). The value provided after the equal signs, decides whether the version of the installed filter will be pined or not.

Version pinning makes sure that the filter is installed with the same version for everyone who runs the project, when they run `regolith install-all`.

For pinned versions you can use semver or SHA of the commit in the git respository:

- Specific version: `regolith install name_ninja==1.2.8`
- SHA: `regolith install name_ninja==adf506df267d10189b6edcdfeec6c560247b823f`

If you don't want to pin the version, you have two options.

- Unpinned Head: `regolith install name_ninja==HEAD` - This makes the install-all command always download the newest commit in the repository.
- Unpinned Latest: `regolith install name_ninja==latest` - This makes the install-all command always download the newest release of the filter.

If you don't specify a version, the `install` command will pick a sensible default. First, it will search for the latest release, if that doesn't exist (in filters without releases), it will select the latest commit in the repository. In both cases, the installed version will be **pinned**.

In your `config.json`, every {ref}`filter definition<filter-definitions>` will include a `version` field, which specifies which version of the filter to use. The version field can contain a semver version, a commit SHA, or the strings `HEAD` or `latest`, matching the version you specified when installing the filter.
