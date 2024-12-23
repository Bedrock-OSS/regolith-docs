(regolith-cache)=
# Regolith Cache

Regolith uses a folder in the user's application data directory to store various caches and the user configuration file. On Windows, you can find this folder at `%localappdata%/regolith`. On other systems, please refer to the Golang documentation of the [os.UserCacheDir](https://pkg.go.dev/os#UserCacheDir) function (the path is the `regolith` subfolder of the result of this function). In later part of this documentation page we will refer to this folder using the Windows path (`%localappdata%/regolith`).

Regolith uses the following caches:
- project-cache
- filter-cache
- resolver-cache


(project-cache)=
# Project Cache
Project cache is a cache used to store the project's files. This is where regolith installs the project's filters and creates the temporary files when it runs.

By default, the project cache is located directly in the project's folder in the `.regolith` folder. This folder is added to the `.gitignore` if you initialize the project with `regolith init`.

If you use the {ref}`use_project_app_data_storage<use-project-app-data-storage>` option in the user configuration, the files will be stored in `%localappdata%/regolith/project-cache` instead.

The project cache can be cleaned with the following command:
```text
regolith clean
```
This works only if you are in the project's folder. It will remove both the `.regolith` folder and the corresponding cache in the `%localappdata%/regolith/project-cache` folder.

If you want to clean all of the project caches from the `%localappdata%/regolith/project-cache` you can run:
```text
regolith clean --user-cache
```
The unintuitive name of the flag is due to the fact that this used to be the only cache that was stored in the user's application data directory. This flag will likely change in the future.

The paths inside the `%localappdata%/regolith/project-cache` are based on the MD5 hash of the project's path in your file system.

(filter-cache)=
# Filter Cache
Filter cache is a cache used by Regolith to store the repositories of the previously installed filters. Thanks to this cache, Regolith can install the filtes faster, because it doesn't have to download the entire repository every time.

The filter cache files are stored in the `%localappdata%/regolith/filter-cache` folder. The paths inside the folder are based on the MD5 hash of the repository URL.

You can clean the filter cache with the following command:
```text
regolith clean --filter-cache
```
Doing that is useful when you have issues with installing a filter. This can happen if the maintainer of the repository force-pushes a new version of the filter making the local cache desynchronized with the remote repository.

(resolver-cache)=
# Resolver Cache
Resolver cache is a cache used by Regolith to store the repositories of the filter resolvers. Storing them locally allows Regolith not to download the filter resolvers every time it needs to install a filter.

The resolver cache files are stored in `%localappdata%/regolith/resolver-cache` folder. The paths inside the folder are based on the MD5 hash of the resolver repository URL.

There is no command-line-based way to clean the resolver cache. If you want to clean it, you need to delete the files manually.
