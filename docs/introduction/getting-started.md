# Getting Started
This tutorial will guide you through basic usage of Regolith. It assumes that you've already installed Regolith. If you haven't, please refer to the {ref}`installation<installation>` page.

At the end of the tutorial, it is shown how to add filter from the internet into your project and run it. Installing filters requires Git, and the filter used as an example runs in Python. If you want to follow allong, you will need get these dependencies. To learn more about getting Git and Python please refer to the {ref}`Additional Dependencies<additional-dependencies>` section.

## Creating a new Project

To create a new project, navigate to a blank folder, and run `regolith init`. This will create a few files:

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
 - `.regolith` is a special folder that regolith uses to store data. You don't need to look here.
 - `packs/BP` stores your behavior pack.
 - `packs/RP` stores your resource pack.
 - `packs/data` is a special folder that filters can use to store data.
 - `config.json` is the configuration file for Regolith.
 - `.gitignore` is a file which tells {ref}`Git source control<git-dependency>` to ignore certain files. It's not a partof of Regolith but we highly recommend using Git to manage your projects.

## Basic Project Configuration

Next, open up `config.json`. We will be configuring a few fields here, for your addon.

```json
{
  "author": "Your name", // Enter your pack name here. (Example: spooky_gravestones)
  "name": "Project name", // Enter your author name here. (example: Bedrock-OSS)
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
You can read more about the `config.json` file in the {ref}`Configuration File<configuration-file>` section.
```

## Adding Pack Files

At this point, you will want to add some files into your regolith project. If you have an existing project, you can copy/paste the files into the `RP` (resource pack) and `BP` (behavior pack) folders. 

If you don't have an addon prepared, you may also create a fresh one directly in your project folder, following the normal rules. Add a `manifest.json`, a `pack_icon.png`, and any other files you want. The files should go directly into the `RP` and `BP` folders, like this:

```text
📂 example-project
    📂 packs
        📂 BP
            📂 entities
                📄 frog.behavior.json
            📄 manifest.json
            🖼️ pack_icon.png
        📂 data
        📂 RP/...
    📄 .gitignore
    📄 config.json
```

```{note}
Regolith supports creating purely resource-pack- or behavior-pack-oriented projects. If your project doesn't have a resource pack or behavior pack, you can simply remove the appropriate field from the `config.json` file, and remove the `RP` or `BP` folder.
```

## Running Regolith

You can run regolith using the following command:
```
regolith run
```
It runs the default {ref}`profile<profiles>`. If unmodified, the `default` profile is set to export files into the `development` target. This means it copies the packs into the `development_behavior_packs` and `development_resource_packs` inside the [com.mojang folder](https://wiki.bedrock.dev/guide/project-setup.html#the-com-mojang-folder).

## Adding your first Filter

```{warning}
Installing filters from the internet requires Git. Additionally, the filter used as an example in this section requires Python to run. You can read more about these dependencies in the {ref}`Additional Dependencies<additional-dependencies>` section.
```

Regolith contains a very powerful filter system, that allows you to write filters in many languages, as well as running existing filters from the internet. For now, we will simply use the {ref}`standard library<standard-library>`, which is a set of filters maintained by Bedrock-OSS.

As an example, we will use the `texture_list` filter, which automatically creates the `textures_list.json` file for you. To learn more about this file, and why automating it is helpful, read [here](https://wiki.bedrock.dev/concepts/textures-list.html).

You can install this filter by running the following command:
```
regolith install texture_list --profile=default
``` 
This command adds the filter to your project, and appends it to the "default" profile.

Alternatively, you can just run `regolith install texture_list`, and manually add the filter to the profile in the `config.json` file. The "default" profile in the config file should look like this:
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
Now, you can re-run `regolith run`. This time, Regolith will not only copy your packs into the `com.mojang` folder, but also create the `textures_list.json` file for you in your resource pack. Every time you run regolith, this file will be re-created, based on your current textures. No need to manually edit it ever again!

```{warning}
If your project doesn't have any textures, than `texture_list.json` will simply create a blank file `[]`. Consider adding some textures to see the filter at work!
```

## What's Next?

Now that you've created your first Regolith project, and installed your first filters, you are well on your way to being a Regolith expert! You should check out the {ref}`standard library<standard-library>`, to see if additional filters might be useful for you.

Otherwise, you can learn about writing {ref}`custom filters<custom-filters>` or dive deeper into Regolith commands by reading about {ref}`Filter Run Modes<filter-run-modes>` and {ref}`Installing and Updating Filters<filter-installation>`.
