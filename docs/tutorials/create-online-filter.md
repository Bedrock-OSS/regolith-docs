(create-online-filter-tutorial)=
# Create Online Filter (Tutorial)
This tutorial will guide you through creating an online Regolith filter using Python. By the end of this tutorial, you'll have a fully functional filter that can be quickly added to any Regolith project using the {ref}`regolith install<installing-filters>` command.

For more details on online filters, you can also refer to the {ref}`Online Filters<online-filters>` section.

## Requirements
Before starting, ensure you have the following tools:
- {ref}`Python<installing-python>`.
- {ref}`Git<git-dependency>`.
- [GitHub account](https://github.com/).

## Instructions
This tutorial assumes you have a basic understanding of Git and GitHub.

**1.** Create a new Git repository.

Create a new repository with a single subfolder in it. The name of the subfolder will be the name of your filter. Let's call it `hello_online_filter`.

**2.** Create a Python file for your filter.

We'll use the same basic filter as in the {ref}`Local Filter Tutorial<create-local-filter-tutorial>`. Create a file named `main.py` inside the `hello_online_filter` folder. (Feel free to name it differently, but ensure you reference it correctly in the `filter.json` file.)

hello_online_filter/main.py:
```python
from pathlib import Path

Path("RP/hello-from-local-filter.txt").write_text("Hello from the resource pack!")
Path("BP/hello-from-local-filter.txt").write_text("Hello from the behavior pack!")
```
This simple script generates two text files, one in the `RP` folder and another in the `BP` folder, each containing a greeting message.

**3.** Create a filter.json file:

hello_online_filter/filter.json:
```json
{
    "description": "My first online filter.",
    "filters": [
        {
            "runWith": "python",
            "script": "./main.py"
        }
    ]
}
```

You can read about the structure of the `filter.json` file in the {ref}`filter.json section<filter-json>` of the documentation.

Note that the path to the main.py file is relative to the filter.json file, not the root of the repository. Both files are in the same folder - hello_online_filter.

**4.** Push your changes to GitHub. Let's assume that your username is YourUsername and the repository name is example-regolith-filters.

**5.** Test installing your filter.

After pushing your filter to GitHub, you can now install it in any Regolith project.

To test the filter, create a new Regolith project and run the following command to install your filter:
```text
regolith install github.com/YourUsername/example-regolith --profile default
```

This will download your filter and add it to the default profile of the project.

Finally, run the project with:
```text
regolith run
```

Regolith should now create two new files, one in the resource pack and one in the behavior pack, containing the greeting messages.

This completes the tutorial. You've successfully created and tested an online Regolith filter!
