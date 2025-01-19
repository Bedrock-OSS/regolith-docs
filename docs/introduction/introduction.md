(introduction)=
# Introduction

## What is Regolith?

Regolith is a pack compiler designed for Minecraft Bedrock Edition.

It introduces the concept of a **project folder** , which contains the resource pack, behavior pack, and a data folder for additional configurations. This structure is ideal for version control, keeping your "source of truth" separate from Minecraft's `com.mojang` folder.

Here is how a newly initialized Regolith project looks like:

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

### Compilation Flow

In the simplest case, Regolith can be used to move your packs from the project folder, into your target location (typically the development folders in `com.mojang`). However, Regolith's true strength lies in its ability to execute {ref}`arbitrary code during this process<safety>`.

We refer to these scripts and programs as {ref}`filters<filters-introduction>`. Here is the flow:
1. The `RP`, `BP`, and `data` folders are copied to a temporary location.
2. Filters are executed in order, modifying the temporary files in place.
3. The contents of `RP` and `BP` are moved to the export location.
4. If configured, specific subfolders within `data` can be saved back into your project.

This compilation flow enables programmatic modifications to your compiled add-on without affecting your source files. Additionally, by saving specific `data` folder subfolders back to your project,it's possible to persistantly store the results of running filters there.

## Why Regolith?

### Extending Pack Syntax
Regolith allows you to create and extend pack syntax. For example, the [subfunctions](https://github.com/Nusiq/regolith-filters/tree/master/subfunctions) filter lets you define functions within functions without needing additional files:

```text
# Some code
function <aaa>:
    # The code of the subfunction
    execute @a ~ ~ ~ function <bbb>:
        # The code of the nested subfunction
# Some other code
```

Regolith's capabilities extend far beyond modifying individual files. You can transform the entire project structure and even use file formats that Minecraft doesn't natively support (such as custom image formats).

As long as you can write a filter to interpret the new structure and compile it into a valid pack, the possibilities are virtually limitless!

### Non-Destructive Editing

Imagine you have a script that iterates over every entity and generates a language-code translation for each one.

For example, your entity `regolith:big_zombie` could be automatically named `Big Zombie`.

Running this script and copying the output into your `en_US.lang` file saves time but introduces a significant issue: **destructive editing** . This happens when tool-generated content and hand-written content are mixed together in the same file.

Now, imagine adding more entities and running the script again. You're left with the tedious task of manually merging the new tool-generated content with any edits you've made to the `en_US.lang` file in the meantime. Regolith eliminates this problem!

A comparable Regolith filter would not suffer from this problem, because you never directly edit tool generated content. Your Regolith project folder contains only human written content, and your `com.mojang` folder contains only tool-generated content.

This separation ensures that as you add new entities, their names are automatically handled without you ever needing to directly edit or even see the `en_US.lang` file again. You don't need to re-run scripts manually or deal with cumbersome merges.

In essence, Regolith layers compiled content over your hand-written content, allowing you to focus on creation without interference from tool-generated data.

```{note}
If this sounds interesting to you, you might be interested in the [name ninja filter](https://github.com/Bedrock-OSS/regolith-filters/tree/master/name_ninja).
```
