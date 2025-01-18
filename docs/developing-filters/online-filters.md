(online-filters)=
# Online Filters

Online filters are filters that are hosted on online Git repositories, typically on GitHub (but not limited to). This is perfect for a filter that you want to make public, or potentially share internally in a team.

Online filters can be installed using the {ref}`regolith install<installing-filters>` command.

## The Structure of an Online Filter Project

To create an online filter, your github project needs to be structured in a certain way. For starters, every filter needs its own folder, at the top of the GitHub project. This folder name is very important, as it will be the name of the filter.

Every filter project should have the following structure:

```text
📂 <root>
  📂 <filter-name>
    📂 data
    📂 test
    📄 filter.json
    📄 <filter-script>
    📄 <other-filter-files>
  📄 <other-project-files>
```

- `<root>` - The root of the repository. The filters must be in direct subfolders of the root.
- `<filter-name>` - The main folder of the filter. Its name will determine the name of the filter.
- `data` - A data folder of the filter (explained later).
- `test` - A test folder of the filter (explained later).
- `filter.json` - The filter configuration file. This file is required for every filter (explained later).
- `<filter-script>` - Every filter has some kind of a script/executable etc. You can place it anywhere inside the filter's folder except the data and test as long as you reference it correctly in the filter.json file.
- `<other-filter-files>` and `<other-project-files>` - You can have any other files you need anywhere in your project.

(filter-json)=
### filter.json

`filter.json` is a special file, which defines some properties of the online filter defines what the filter does when it is run.

Example:
```json
{
  "description": "A Hello World Filter - this will be displayed as a description on website pages.",
  "exportData": true,
  "filters": [
    {
      "runWith": "python",
      "script": "./hello_world.py"
    }
  ]
}
```

#### description: string
The description property is optional and is the only one that doesn't affect the behavior of the filter. It's a convention for writing a machine-readable description of the filters that can be used by web scrapers that search for the filters on GitHub. You can read more about making your filter discoverable in the {ref}`Publishing Filters<publishing-filters>` section.

(filter-property-export-data)=
#### exportData: bool

The exportData property changes how Regolith handles the {ref}`data folder<data-folder>` of the filter when you {ref}`run Regolith<running-filters>`. It allows the destructive modification of the data folder of the filter. This applies to any changes, including those made by other filters.

Under the hood, when Regolith finishes running on the copy of the project files, it exports the data folders of the filters that use the exportData property back to the sorurce files. This happens only after successful runs, so it's safer than it would be if the changes were made directly to the source files.

This feature was added to let the filters remember their state between runs. Most of the filters don't need this feature, so moving the files back and forth would be a waste of processing time and the `exportData` property is now disabled by default.

```{warning}
Currently the ability to export data is unique to the online filters. The local filters can't use this feature, which makes the development of the filters that modify their data folder more difficult.
```

#### filters: list

The filter property is used to specify the {ref}`fitler definitions of your online filter<online-filter-definition>`.

(online-filters-data-folder)=
## Data Folder

If you need some default configuration files for your remote filter, you can create a folder called data in your filter folder. Here, you can store your default configuration files. When a user runs `regolith install`, this data folder will be moved into their data folder, namespaced under the name of the filter. This happens only if the user doesn't already have a data folder with the same name as the filter. This way, Regolith prevents overwriting the user's data specific to their project.

You can learn more about this flow {ref}`here<data-folder>`.

## Test Folder

The test folder is a special folder in the filter project intended for {ref}`creating tests<testing-filters>` for the filters. Regolith doesn't have any special commands for running tests so its use may depend on the filter's author. Regolith treats the test folder differently than other content of the filter during the {ref}`installation process<installing-filters>`. The content of the test folder is not copied to the {ref}`project cache<project-cache>` so if you're devloping a filter, don't make it rely on the content of the test folder, when it runs the files won't be there.
