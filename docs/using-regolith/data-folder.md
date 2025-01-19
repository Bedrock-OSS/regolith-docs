(data-folder)=
# Data Folder
The `data` folder in a Regolith project is a special directory designed to store files used by filters that don't belong in the `BP` (behavior pack) or `RP` (resource pack) folders. By default, the `data` folder is located at `./packs/data`, but its location can be customized using the {ref}`dataPath<project-config-data-path>` setting in the project configuration file.

## Filter Data
Typically, the `data` folder contains subfolders corresponding to the names of the filters installed in the project. However, you're free to add files directly to the root of the `data` folder or create additional subfolders for other purposes.

Naming subfolders to match the names of the filters isn't just a matter of convention - it has practical significance:

1. **Default Data Files** : Some filters include {ref}`default data files<online-filters-data-folder>` that are automatically copied into the `data` folder when the filter is {ref}`installed<installing-filters>` for the first time. These files are placed in a subfolder named after the filter.
2. **Editable Data Folders** : Certain filters {ref}`register their data folders as editable<filter-property-export-data>`. When this happens, any changes made to these folders during {ref}`running filters<running-filters>` are saved to the project. This feature allows filters to store and update persistent data between runs.

As a user, you don't have to worry about these details too much:
- The `install` command will **never overwrite**  existing filter data, ensuring your customizations are preserved.
- Most filters do **not**  register their data as editable. If a filter does, this is typically noted in its documentation.
