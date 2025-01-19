# Help & Autocompletion

## Help Command
Regolith includes a built-in help command to assist with exploring its features. You can use this to view the list of available commands, along with their descriptions. To access help, run the following command:
```text
regolith help
```
If you'd like to learn more about a specific subcommand, such as `regolith run`, you can get detailed information by running:

```text
regolith help run
```

This will provide you with an overview of the command, along with a full list of its flags and their descriptions.

## Autocompletion
Regolith's CLI is built using [Cobra](https://github.com/spf13/cobra), which provides support for autocompletion. Cobra can generate autocompletion scripts for various shells, including Bash, Zsh, Fish, and PowerShell. To generate an autocompletion script for your shell, run:
```text
regolith completion <your-shell>
```

For instance, to generate the autocompletion script for PowerShell, use:
```powershell
regolith completion powershell
```

This command will generate the script and output it to the console.

To apply the script instantly within the current PowerShell session, run:

```powershell
regolith completion powershell | Out-String | Invoke-Expression
```
This will remain active until the end of your session. To make it permanent, add the script's content to your PowerShell profile. You can find the profile path in the `$PROFILE` variable.

For other shells, the process is similar: just replace `powershell` with your shell name and place the generated script in the appropriate location for your shell.

```{note}
The autocompletion feature in Regolith is currently very basic. It provides autocompletion only for subcommands. It doesn't provide autocompletion for the flags and arguments.
```
