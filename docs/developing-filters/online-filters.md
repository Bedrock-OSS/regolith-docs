(online-filters)=
# Online Filters

Online filters are filters that are hosted on online Git repositories, typically on GitHub (but not limited to). This is perfect for a filter that you want to make public, or potentially share internally in a team.

You can install online filters using the {ref}`regolith install<installing-filters>` command.

If you wnat to learn by example, you can check out the {ref}`Create Online Filter Tutorial<create-online-filter-tutorial>`. It gives you a quick step-by-step guide but doesn't go into the details of the filter development that you can find here.

## Structure of an Online Filter Project
To create an online filter, the repository must follow a specific structure. Each filter must have its own folder at the root of the repository. The folder name becomes the filter's name.

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

- `<root>`: Root of the repository. Filters must be in direct subfolders of the root.
- `<filter-name>`: Main folder of the filter. Its name determines the filter name.
- `data`: The data folder of the filter (explained later).
- `test`: The test folder of the filter (explained later).
- `filter.json`: Mandatory filter configuration file (explained below).
- `<filter-script>`: Script or executable for the filter. It must be referenced correctly in the `filter.json` file.
- `<other-filter-files>` and `<other-project-files>`: You can have any other files you need anywhere in your project.

(filter-json)=
### filter.json
The `filter.json` file is a critical component of online filters. It defines the filter's properties and behavior.

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

Under the hood, when Regolith finishes running on the copy of the project files, it exports the data folders of the filters that use the `exportData` property back to the sorurce files. This happens only after successful runs, so it's safer than it would be if the changes were made directly to the source files.

This feature was added to let the filters remember their state between runs. Most of the filters don't need this feature. Moving the files back and forth would be a waste of processing time and the `exportData` property disabled by default.

```{warning}
Currently the ability to export data is unique to the online filters. The local filters can't use this feature, which makes the development of the filters that modify their data folder more difficult.
```

#### filters: list
Defines the {ref}`filter definitions of your online filter<online-filter-definition>`.

(online-filters-data-folder)=
## Data Folder
The `data` folder stores default configuration files for the filter. When a user runs `regolith install`, the contents of this folder are copied to their project's `data` folder under a namespace matching the filter name. This happens only if the user doesn't already have a data folder with the same name as the filter. This way, Regolith prevents overwriting the user's data specific to their project.

You can learn more about this flow {ref}`here<data-folder>`.

## Test Folder
The `test` folder is intended for {ref}`creating tests<testing-filters>` for the filter. It is treated differently during the {ref}`installation process<installing-filters>` than any other folder. The content of the test folder is not copied to the {ref}`project cache<project-cache>` so if you're devloping a filter, don't make it rely on the content of the test folder, when it runs the files won't be there.
