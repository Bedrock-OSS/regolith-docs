(filters-introduction)=
# Filters Introduction

## What is a Filter?
A filter is a program or script that you can add to your {ref}`project's compilation process<running-filters>`. Filters are the core of Regolith and are what make it so powerful.

You can think of a filter as the ability to run arbitrary code during the compilation process. This allows you to accomplish a number of tasks:

- Linting and error checking.
- Code generation/automation.
- Interpreting custom syntax.


## Online and Local Filters
Filters fall into two categories - online and local.

Using online filters is best for beginners. You can simply {ref}`install them<installing-filters>` using `regolith install` command and they should be ready to use. Many of these filters have already been written, and are included as part of the [standard library](https://github.com/Bedrock-OSS/regolith-filter-resolver?tab=readme-ov-file#standard-filters) and [community filters](https://github.com/Bedrock-OSS/regolith-filter-resolver?tab=readme-ov-file#community-filters).

If you are more experienced, you can write your own filters in your favorite programming language. You can read more about developing {ref}`local<local-filters>` and {ref}`online<online-filters>` filters in their respective sections.
