(shell-filters)=
# Shell Filters

Shell filters allow you to run arbitrary shell commands. This is useful for running scripts that are not natively supported in Regolith.

## Shell Filter Definition

The structure of the Shell filter definition is described below. You can read how to use it in the {ref}`Filter Definition<filter-definition>` section.

```json
{
  "runWith": "shell",
  "command": "echo 'hello world'"
}
```

- `runWith` - always set to `shell`, marks this filter as a Shell filter.
- `command` - the shell command to run.
