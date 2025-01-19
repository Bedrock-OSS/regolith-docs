(getting-started)=
# Getting Started

```{warning}
Regolith is a command-line application. It assumes you have some familiarity with navigating and using the command line. If you need a refresher, check out [this tutorial](https://tutorial.djangogirls.org/en/intro_to_command_line/).
```

This tutorial will guide you through the basic usage of Regolith. It assumes that you've already installed Regolith. If not, please refer to the {ref}`installation<installation>` page.

By the end of this tutorial, you'll learn how to add and run a filter from the internet in your project. Installing filters requires Git, and the example filter runs in Python. If you want to follow along, ensure you have these dependencies installed. For Git installation instructions, see the {ref}`Additional Dependencies<additional-dependencies>` section. For Python installation instructions, refer to the {ref}`Python Filters<python-filters>` section.

## Creating a New Project

To create a new project, navigate to an empty folder and run:
```text
regolith init
```

This will create a few files:
```text
📂 example-project
    📂 .regolith
    📂 packs
        📂 BP
        📂 data
        📂 RP
    📄 .gitignore
    📄 config.json
```

In short:
- `.regolith`: A special folder Regolith uses to store its data. You typically don't need to access this.
- `packs/BP`: The folder for your behavior pack.
- `packs/RP`: The folder for your resource pack.
- `packs/data`: A special folder filters can use to store additional data.
- `config.json`: Regolith's configuration file.
- `.gitignore`: A file that tells {ref}`Git<git-dependency>` to ignore specific files. While not part of Regolith itself, using Git to manage your projects is highly recommended.

## Basic Project Configuration

Next, open up `config.json`. We will be configuring a few fields here, for your addon.

```json
{
  "author": "Your name", // Replace with your name (e.g., Bedrock-OSS)
  "name": "Project name", // Replace with your project name (e.g., spooky_gravestones)
  "packs": {
    "behaviorPack": "./packs/BP",
    "resourcePack": "./packs/RP"
  },
  "regolith": {
    "dataPath": "./packs/data",
    "filterDefinitions": {},
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

Later on you can play with the additional configuration options, but for now, just set a project name, and author name (marked in the snipped above with comments).

Setting the name of the project is important, because Regolith often uses it to generate the names of the exported folders, for example, resource pack and behavior pack folders in the {ref}`"development" export target<export-targets>` by default use the project name as a prefix.

```{note}
For more details about the `config.json` file, refer to the {ref}`Configuration File<project-config-file>` section.
```


## Adding Pack Files

At this stage, you'll want to populate your Regolith project with files.

If you have an existing addon, copy and paste your files into the `RP` (resource pack) and `BP` (behavior pack) folders within your project directory.

If you don't have an addon prepared, you can use files from the [example project prepared for this tutorial](https://github.com/Bedrock-OSS/regolith-docs-tutorial-resources/releases/tag/1.4.1-getting-started).

1. Download the `RP.zip` and `BP.zip` files from the link above.
2. Extract the contents of `RP.zip` into the `RP` folder.
3. Extract the contents of `BP.zip` into the `BP` folder.

Alternatively, you can download the complete, final version of the project as `getting-started-full-project.zip`.

```{note}
Regolith supports projects that focus solely on resource packs or behavior packs. If your project doesn't have one of these, you can remove the corresponding field (`behaviorPack` or `resourcePack`) from the `config.json` file and delete the unused `RP` or `BP` folder.
```

## Running Regolith

To run Regolith, use the following command:
```text
regolith run
```
By default, this runs the `default` {ref}`profile<profiles>`, which (if unmodified) is configured to export files into the `development` target. This means your packs will be copied into the `development_behavior_packs` and `development_resource_packs` folders within the [com.mojang folder](https://wiki.bedrock.dev/guide/project-setup.html#the-com-mojang-folder).

## Adding Your First Filter

Regolith features a powerful filter system that supports writing custom filters in various programming languages and running pre-existing filters from the internet. For now, we'll use the [Standard Filters Library](https://github.com/Bedrock-OSS/regolith-filter-resolver?tab=readme-ov-file#standard-filters), a collection of filters maintained by the creators of Regolith, Bedrock-OSS.

As an example, we will use the `texture_list` filter, which automatically creates the `textures_list.json` file for you. To learn more about this file, and why automating it is helpful, read [here](https://wiki.bedrock.dev/concepts/textures-list.html).

To install the `texture_list` filter, run the following command:
```text
regolith install texture_list --profile=default
```
This command installs the filter and appends it to the "default" profile in your `config.json` file.

If you prefer, you can install the filter without assigning it to a profile immediately:
```text
regolith install texture_list
```

Then, manually update the `default` profile in the `config.json` file to include the filter:
```json
"default": {
  "export": {
    "readOnly": false,
    "target": "development",
    "build": "standard"
  },
  "filters": [
    {
      "filter": "texture_list"
    }
  ]
}
```

Now, you can re-run `regolith run`. This time, in addition to copying your packs into the `development` folders in the `com.mojang` folder, Regolith will also generate the `textures_list.json` file in your resource pack. Each time you run Regolith, this file will be re-created based on your current textures. You'll never need to manually edit it again!

```{warning}
If your project doesn't contain any textures, the `texture_list.json` file will be generated as an empty file (`[]`). Add some textures to your project to see the filter in action!
```
