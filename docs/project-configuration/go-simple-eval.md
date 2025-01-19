(go-simple-eval)=
# Go-Simple-Eval
Regolith uses the [go-simple-eval library](https://github.com/stirante/go-simple-eval/) to evaluate expressions within the project configuration file:
- The `when` expression in the {ref}`filter settings<project-config-filters-properties>`.
- The `rpName` and `bpName` in some of the {ref}`export targets<export-targets>`.

## Syntax

Go-simple-eval offers a simple syntax supporting basic operations commonly found in programming languages.

```{warning}
This section does not provide a full reference for go-simple-eval, but the features outlined here are sufficient for use in Regolith.
```

### Operators
- **Comparison operators** : `==`, `!=`, `<`, `<=`, `>`, `>=`
- **Logical operators** : `&&`, `||`, `!`
- **Math operators** : `+`, `-`, `*`, `/`
- **String concatenation** : `+`

### Parentheses
Use parentheses to group expressions, such as `(1 + 2) * 3`.

### Strings
Strings are enclosed in single quotes, like `'This is a string'`.

### Reserved Words
- `true` and `true` and `false`: Reserved for boolean values.
- `null`: Reserved for null values.

## Variables

Regolith provides several variables for use in expressions:
- `project.name`: The name of the project.
- `project.author`: The author of the project.
- `os`: The host operating system, retrieved from `runtime.GOOS` (e.g., `linux`, `windows`, `darwin`).
- `arch`: The host architecture, retrieved from `runtime.GOARCH` (e.g., `amd64`, `arm64`).
- `debug`: Indicates whether Regolith is running in debug mode (i.e., when the `--debug` flag is used).
- `version`: The version of Regolith.
- `profile`: The name of the profile being run.
