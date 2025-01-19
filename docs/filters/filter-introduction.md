(filters-introduction)=
# Filters Introduction

## What is a Filter?
A filter is a program or script that you can integrate into your {ref}`project's compilation process<running-filters>`. Filters are the foundation of Regolith's functionality and the source of its power.

Essentially, a filter allows you to execute arbitrary code during the compilation process. This flexibility enables a wide range of tasks, such as:

- Linting and error checking.
- Code generation/automation.
- Interpreting custom syntax.

## Online and Local Filters
Filters are categorized into two types: **online filters**  and **local filters** .

Using online filters is best for beginners. You can simply {ref}`install them<installing-filters>` using `regolith install` command and they should be ready to use. Many of these filters have already been written, and are included as part of the [standard library](https://github.com/Bedrock-OSS/regolith-filter-resolver?tab=readme-ov-file#standard-filters) and [community filters](https://github.com/Bedrock-OSS/regolith-filter-resolver?tab=readme-ov-file#community-filters).

If you're more experienced or need custom functionality, you can write your own filters using your preferred programming language. Local filters allow you to tailor the compilation process to meet the unique requirements of your project.

For more information, check out the guides on developing {ref}`local filters<local-filters>` and {ref}`online filters<online-filters>`.
