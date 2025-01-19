(regolith-cache)=
# Regolith Cache
Regolith stores various caches and the user configuration file in a folder within the user's application data directory. On Windows, this folder is located at `%localappdata%/regolith`. For other systems, refer to the Golang documentation for the [os.UserCacheDir](https://pkg.go.dev/os#UserCacheDir) function (the path is the `regolith` subfolder of the directory returned by this function). In following sections of this documentation page, we will refer to this folder using the Windows path (`%localappdata%/regolith`).

Regolith uses the following caches:
- project-cache
- filter-cache
- resolver-cache

(project-cache)=
## Project Cache
The project cache stores your project's files, including installed filters and temporary files created when running Regolith.

By default, the project cache is located in the `.regolith` folder within the project's directory. This folder is automatically added to the `.gitignore` if you initialize the project with `regolith init`.

If you use the {ref}`use_project_app_data_storage<use-project-app-data-storage>` option in the user configuration, the cache will be stored in `%localappdata%/regolith/project-cache` instead.

You can clean the project cache with the following command:
```text
regolith clean
```
This command only works when you're in the project's folder. It removes both the `.regolith` folder and the corresponding cache in `%localappdata%/regolith/project-cache`.

To clean all project caches from the `%localappdata%/regolith/project-cache`, you can run:
```text
regolith clean --user-cache
```
The name of the flag is unintuitive because this was once the only cache stored in the user's application data directory. It may be renamed in the future

The paths inside `%localappdata%/regolith/project-cache` are based on the MD5 hash of your project's file path.

(filter-cache)=
## Filter Cache
The filter cache stores repositories of previously installed filters. By keeping these repositories locally, Regolith can install filters more quickly, as it doesn't need to download the entire repository every time.

The filter cache is located in `%localappdata%/regolith/filter-cache`, and the paths inside the folder are based on the MD5 hash of the repository's URL.

To clean the filter cache, run:
```text
regolith clean --filter-cache
```

This is helpful if you encounter issues with installing a filter, such as when the repository maintainer force-pushes a new version of the filter, causing a desynchronization between the local cache and the remote repository.

(resolver-cache)=
## Resolver Cache
The resolver cache stores repositories of filter resolvers. By caching them locally, Regolith avoids downloading the resolvers each time it installs a filter.

The resolver cache files are stored in the `%localappdata%/regolith/resolver-cache` folder. The paths inside the folder are based on the MD5 hash of the resolver repository's URL.

Currently, there is no command-line method to clean the resolver cache. To clear it, you'll need to delete the files manually.
