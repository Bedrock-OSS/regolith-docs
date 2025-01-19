(create-local-filter-tutorial)=
# Create Local Filter (Tutorial)
This step-by-step tutorial explains how to create a basic local Regolith filter using Python. By the end of this tutorial, you'll have a working filter that generates two `hello-from-local-filter.txt` files in your resource and behavior packs.

You can also refer to the {ref}`Local Filters<local-filters>` section for more detailed information.

## Requirements
Before starting, ensure Python is installed on your system. For installation instructions, refer to the {ref}`Python Filters<installing-python>` page.

## Instructions
**1.** Create a new Regolith project.

{ref}`Initialize a new project<getting-started>` by running the following command in a blank folder:
```
regolith init
```

**2.** Create a Python file for your filter.

Create a folder named `filters` in the root of your project. Inside this folder, create a new Python file, `hello_filter.py` (you can choose a different path if you like, but it's a good practice to organize filters this way).

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

By default, the export target is set to `development`. If you prefer to export the files to a `build` folder in the project root for testing, you can change the target to `local`.

**5.** Run the filter.

Now that you've set up the filter, run the Regolith project. The `hello-from-local-filter.txt` files will be created in both the resource pack and behavior pack directories with their respective greeting messages.
