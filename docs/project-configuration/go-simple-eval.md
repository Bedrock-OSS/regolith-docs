(go-simple-eval)=
# Go-Simple-Eval

Regolith uses the [go-simple-eval library](https://github.com/stirante/go-simple-eval/) to evaluate some expressions in the project configuration file:
- The `when` expression in the {ref}`filter settings<project-config-filters-properties>` object.
- The `rpName` and `bpName` in some of the {ref}`export targets<export-targets>`.

## Syntax

Go-simple-eval uses a simple syntax that supports basic operations you would expect from a programming language.

```{warning}
This is not a full documentation of go-simple-eval, but the features explained here should be enough for using it in Regolith.
```

### Operators
- Comparison operators: `==`, `!=`, `<`, `<=`, `>`, `>=`
- Logical operators: `&&`, `||`, `!`
- Math operators: `+`, `-`, `*`, `/`
- String concatenation: `+`

### Parentheses
You can use parentheses to group expressions like this: `(1 + 2) * 3`.

### Strings
Strings must be enclosed in single quotes like this: `'This is a string'`.

### Reserved Words
- `true` and `false` are reserved words for boolean values.
- `null` is a reserved word for null values.

## Variables

Regolith provides some variables that you can use in the expressions:

- `project.name` - The name of the project.
- `project.author` - The author of the project.
- `os` - The host operating system. The value is retrieved from `runtime.GOOS`, which means that based on the host system, the value can be `linux`, `windows`, `darwin`, etc.
- `arch` - The host architecture. The value is retrieved from `runtime.GOARCH`, which means that based on the host system, the value can be `amd64`, `arm64`, etc.
- `debug` - whether regolith is running in debug mode or not (using the `--debug` flag).
- `version` - The version of regolith.
- `profile` - The name of the profile being run.
