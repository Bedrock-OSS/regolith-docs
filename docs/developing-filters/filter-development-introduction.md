(filter-development-introduction)=
# Filter Development Introduction

This page gives general tips about developing filters for Regolith. For more specific information about {ref}`online<online-filters>` and {ref}`local<local-filters>` filters, please see the dedicated pages.

If you aren't a developer, and are looking for information on how to use filters, please see the {ref}`Filters Introduction<filters-introduction>` page.

## The Working Directory of Filters

Filters are run in the temporary directory that contains 3 subdirectories - RP, BP, and data. Depending on the user's settings (specifically the {ref}`use_project_app_data_storage<use-project-app-data-storage>`) this may be outside of the project directory. The files in the temporary directory are copies of the files in the project.

When developing filters, you don't need to worry about finding the paths to the project files because Regolith sets the working directory for you and the structure of the temporary directory is always the same. You can simply find your behavior pack in `./BP/`, resource pack in `./RP/`, and data in `./data/`.

## Non-Destructive Editing

Since filters arn not actually editing the project files, you don't need to worry about leaving your project in a broken state in case of an error. Regolith never applies the changes your filter makes to `RP` and `BP` directories, and changes to the `data` directory require {ref}`explicit permission<filter-property-export-data>` in the filter configuration, and are only applied after a successful run.

## Accessing Files Outside of the Temporary Directory Using Environment Variables

While modifying files outside of the temporary directory goes against the non-destructive editing philosophy of Regolith, sometimes it's necessary. If your filter needs to access files outside of the temporary directory, Regolith provides some environment variables to help you with that. These are active for every filter run by Regolith:

 - `FILTER_DIR` - This environment variable contains an absolute path to the filter directory, inside the {ref}`project cache<project-cache>`. For local filters, this is where the filter script is stored. For online filters, this is the path where the filter.json file is.
 - `ROOT_DIR` - This environemnt variable contains an absolute path to the project root directory, where config.json file is.

Be aware that if your filter crashes while editing files outside of the temporary directory, there is no mechanism to revert the changes. Your filter will need to handle this itself.
