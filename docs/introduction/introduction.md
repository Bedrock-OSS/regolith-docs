(introduction)=
# Introduction

## What is Regolith?

Regolith is a pack compiler for the Bedrock Edition of Minecraft.

Regolith introduces the concept of a **project folder**, that includes the resource pack, behavior pack, and data folder that can be used for additional configuration. This structure is great for version control, and allows you to keep your "source-of-truth" outside of Minecraft's `com.mojang` folder.

Here is what a newly initialized Regolith project looks like:

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

In the simplest case, Regolith can be used to move your packs from the project folder, into your target location (usually the development folders in `com.mojang`). Each time you run regolith, the packs will be moved over, and updated.

However, Regolith's real value preposition is the ability to run {ref}`arbitrary code during this copy<safety>`.

We refer to these scripts and programs as {ref}`filters<filters-introduction>`. Here is the flow:
1. `RP`, `BP` and `data` folder are copied into a temporary location.
2. Every filter is executed in-order, editing temporary files in-place.
3. The contents of `RP` and `BP` are moved into your export location
4. If configured, some of the subfolders within `data` can be moved back into your project.

This compilation flow allows you to make programmatic changes to your compiled addon, without effecting your source files. Since the data folder can be saved back to your project, it's possible to persistantly store the results of running filters there.

## Why Regolith?

### Extending the Packs Syntax

Regolith allows you to create and extend packs syntax. For example, the [subfunctions](https://github.com/Nusiq/regolith-filters/tree/master/subfunctions) filter allows you to define functions within functions, without creating an additional file:

```
# Some code
function <aaa>:
    # The code of the subfunction
    execute @a ~ ~ ~ function <bbb>:
        # The code of the nested subfunction
# Some other code
```

Regolith's capablities go beyond chaning the individual files. You can change entire structure of the project and use files that otherwise would not be supported by Minecraft (for example, custom image formats).

As long as you can write a filter to interpret the new structure, and compile it into valid pack, then anything goes!

### Non-Destructive Editing

Imagine you have a script that loops over every entity, and creates some language-code translation for it.

Lets say your entity `regolith:big_zombie` becomes named `Big Zombie`.

If you run this script, and copy the files into your `en_US.lang`, you've saved yourself a lot of time, but you've also introduced a problem: You've *destructively edited your pack*. What this means, is that you have mixed up your tool-generated content, with your hand-written content.

Imagine you add more entities, and run your script again: Now you are in the painful position of "merging" the new tool generated content, with your resource pack's `en_US.lang` file, which you may have edited in the interim.

This is called *destructive editing*, and Regolith fixes it!

A comparable Regolith filter would not suffer from this problem, because you never directly edit tool generated content. Your Regolith project folder contains only human written content, and your `com.mojang` folder contains only tool-generated content.

This means as you add new entities, the names will be handled for you, without you ever seeing the names in `en_US.lang`, or needing to re-run the script!

In other words, Regolith adds compiled content on top of your hand written content, leaving you free to create your content, without working around tool-generated content.

```{note}
If this sounds interesting to you, you might be interested in the [name ninja filter](https://github.com/Bedrock-OSS/regolith-filters/tree/master/name_ninja).
```
