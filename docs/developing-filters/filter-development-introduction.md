(filter-development-introduction)=
# Filter Development Introduction
This page provides general guidelines for developing filters in Regolith. For detailed information about creating {ref}`online<online-filters>` and {ref}`local<local-filters>` filters, refer to their respective pages.

If you're not a developer and are looking for instructions on using filters, visit the {ref}`Filters Introduction<filters-introduction>` page instead.

(the-working-directory-of-filters)=
## The Working Directory of Filters
Filters are executed in a temporary directory containing three subdirectories: `RP`, `BP`, and `data`. Depending on the user's settings (specifically {ref}`use_project_app_data_storage<use-project-app-data-storage>`), this directory may be located outside the project folder. Files in the temporary directory are copies of the project files.

As a developer, you don't need to manually locate the paths to project files. Regolith automatically sets the working directory for your filter. The directory structure is consistent, with behavior pack files in `./BP/`, resource pack files in `./RP/`, and data files in `./data/`.

## Non-Destructive Editing
Since filters aren't actually editing the project files, you don't need to worry about leaving your project in a broken state in case of an error. Regolith never applies the changes your filters make to `RP` and `BP` directories, and changes to the `data` directory require {ref}`explicit permission<filter-property-export-data>` in the filter configuration, and are only applied after a successful run.

## Accessing Files Outside the Temporary Directory Using Environment Variables
Although modifying files outside the temporary directory goes against Regolith's non-destructive editing philosophy, it may be necessary in specific scenarios. To facilitate this, Regolith provides the following environment variables, which are set for every filter run:

- `ROOT_DIR`: Contains the absolute path to the project's root directory (where the `config.json` file resides).
- `FILTER_DIR`: Contains the absolute path to the directory where the filter is defined. For online filters, this points to the directory containing the `filter.json` file within the {ref}`project cache<project-cache>`. For local filters, it is the same as `ROOT_DIR`, as their definition resides in the `config.json` file.

If your filter interacts with files outside the temporary directory and an error occurs, Regolith cannot automatically revert those changes. Your filter should include mechanisms to handle such scenarios and ensure file integrity.
