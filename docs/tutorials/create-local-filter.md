(create-local-filter-tutorial)=
# Create Local Filter (Tutorial)

This is a step-by-step tutorial that explains how to create a basic local Regolith filter using the Python programming language. At the end of this tutorial, you will have a working filter that creates two hello-from-local-filter.txt files in resource and behavior packs.

You can also read about the local filters in the {ref}`Local Filters<local-filters>` section of the documentation.

## Requirements

Before you can begin, you need to ensure that Python is installed on your system. You can find the installation instructions on the {ref}`Python Filters<installing-python>` page.

## Instructions

**1.** Create a new Regolith project.

{ref}`Initialize a new project<getting-started>` by running the following command in a blank folder:
```
regolith init
```

**2.** Create a Python file for your filter.

Create a new folder in the root of your project called filters. Inside this folder, create a new Python file called `hello_filter.py`. You can pick any other name and puting the script in the filters folder is optional, but it is a good practice to keep your filters organized.

filters/hello_filter.py:
```python
from pathlib import Path

Path("RP/hello-from-local-filter.txt").write_text("Hello from the resource pack!")
Path("BP/hello-from-local-filter.txt").write_text("Hello from the behavior pack!")
```
This simple script creates two files. One in RP and one in BP, both containing a greeting message. Note that we are using `RP/` to access the resource pack and `BP/` to access the behavior pack. You can read more about it in the {ref}`Filter Development Introduction<filter-development-introduction>` section.

**3.** Register your filter in the project configuration.

Simply add a new object to `filterDefinitions` in your `config.json` file.
```json
{
    "author": "Your name",
    "name": "Project name",
    "packs": {
        "behaviorPack": "./packs/BP",
        "resourcePack": "./packs/RP"
    },
    "regolith": {
        "dataPath": "./packs/data",
        "filterDefinitions": {
            // This part is not generated with "regolith init"
            "hello_filter": {
                "runWith": "python",
                "script": "./filters/hello_filter.py"
            }
        },
        "formatVersion": "1.4.0",
        "profiles": {
            "default": {
                "export": {
                    "build": "standard",
                    "readOnly": false,
                    "target": "development"
                },
                "filters": []
            }
        }
    }
}
```

**4.** Add the filter to the default profile.

Edit the `profiles` section of the config file to include the reference to your filter.
```json
"profiles": {
    "default": {
        "export": {
            "build": "standard",
            "readOnly": false,
            "target": "development"
        },
        "filters": [
            {
                "filter": "hello_filter"
            }
        ]
    }
}
```

Note that the default {ref}`export target<export-targets>` is `development`. If you change it to `local`, the files will be exported to a `build` folder in the project root which is useful if you just want to see how the filter works.

**5.** Run the filter.

That's it! You successfully created a local filter. The resource and behavior packs created by Regolith should now contain the `hello-from-local-filter.txt` files with the greeting messages.
