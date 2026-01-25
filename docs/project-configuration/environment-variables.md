(environment-variables)=
# Environment Variables

Regolith supports usage of environment variables in various contexts:
- {ref}`Go-Simple-Eval expressions<go-simple-eval>`
- {ref}`Filters<filters-introduction>` can access them in their code.
- The {ref}`preShell and posShell<project-config-pre-and-post-shell>` properties of profiles can set them using shell commands.

This section provides an overview of how to work with environment variables in Regolith.

## .env File

Regolith supports loading environment variables from a `.env` file located in the root of your project directory. This file should contain key-value pairs in the format `KEY=VALUE`, one per line. For example:

```
SOME_VAR=Hello, World!
SOME_OTHER_VAR=Some other value
```

## --env Flag
The `--env` flag can be used with any Regolith command. It allows you to specify a custom path to a `.env` file.

For example if you want to {ref}`run<running-filters>` regolith with a custom `.env` file, you can use the following command:

```text
regolith run --env ./path/to/env/file
```
