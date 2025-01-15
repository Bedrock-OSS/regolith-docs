(data-folder)=
# Data Folder

The `data` folder in a Regolith project is a special folder designed to store the files of the filters that don't belong to `BP` or `RP` folders. By default it is located in `./packs/data`, but you can change it by using the {ref}`dataPath<project-config-data-path>` setting in the project configuration file.


## Filter Data

The data folder typically contains subfolders that correspond to the filters installed in the project, but if you need, nothing stops you from adding files directly to its root or creating subfolders for other purposes.

Using the same names of the folders that match the names of the filters isn't just a convention. It has some practical implications:

1. Some filters provide {ref}`default data files<online-filters-data-folder>` that will be copied into the data folder when you {ref}`install<installing-filters>` them for the first time.
2. Some filters {ref}`may register their data folder as editable<filter-property-export-data>`. This means that all changes applied to their data folder during {ref}`running filters<running-filters>` will be saved in the project.

As a user, you don't have to worry about these details too much. The install command will never overwrite filter's data if you already have it, and the majority of the filters doesn't register their data as editable; if they do it is most likely mentioned their documentation.
