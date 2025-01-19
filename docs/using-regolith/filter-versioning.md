(filter-versioning)=
# Filter Versioning
Regolith filters are versioned either using versions assigned by their creators with [semantic versioning](https://semver.org/)  or by the SHA values of commits in their GitHub repository. When you install a filter, Regolith saves the version of the filter in your {ref}`config file<project-config-file>` by default.

## Version Pinning
When installing, you can optionally include a version key after two equals signs (`==`). The value provided after the equal signs decides whether the version of the installed filter will be pined or not.

Version pinning makes sure that the filter is installed with the same version for everyone who runs the project, when they run `regolith install-all`.

For pinned versions you can use semver or SHA of the commit in the git respository:
- Specific version: `regolith install name_ninja==1.2.8`
- Commit SHA: `regolith install name_ninja==adf506df267d10189b6edcdfeec6c560247b823f`

If you prefer not to pin the version, you have two options:

- Unpinned Head: `regolith install name_ninja==HEAD` - This makes the install-all command always download the newest commit in the repository.
- Unpinned Latest: `regolith install name_ninja==latest` - This makes the install-all command always download the newest release of the filter.

If you don't specify a version, the `install` command will automatically choose a sensible default. It will first check for the latest release, and if no release is found (in the case of filters without releases), it will select the latest commit from the repository. In both cases, the installed version will be **pinned**.

In your `config.json`, each {ref}`filter definition<filter-definitions>` will include a `version` field that specifies which version of the filter to use. This field can contain a semver version, commit SHA, or the strings `HEAD` or `latest`, corresponding to the version you specified when installing the filter.
