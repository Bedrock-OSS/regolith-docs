# Help & Autocompletion

## Help Command

Regolith has a build in help command to explore its features. You can use it to get the list of the commands with their explanation. To get help simply run the following command:

```
regolith help
```

If you want to learn about specific subcommand for example `regolith run`, run `regolith help <subcommand>` like this:

```
regolith help run
```

This way you can read about the  command and get a full list of its flags, with their explanation.

## Autocompletion

Regolith CLI is implemented with [Cobra](https://github.com/spf13/cobra) which provides an autocompletion feature. Cobra supports generating autocompletion scripts for Bash, Zsh, Fish, and PowerShell. To generate the autocompletion script for your shell you need to run `regolith completion <your-shell>`.

For example, to generate the autocompletion script for PowerShell run:

```powershell
regolith completion powershell
```
This command will generate the autocompletion script for PowerShell and print it to the console.

In PowerShell, you can instantly run the script by running:

```powershell
regolith completion powershell | Out-String | Invoke-Expression
```
This will work until the end of the session. If you want to make it permanent, you can add the content of the script to your PowerShell profile. In PowerShell, the profile path is stored in the `$PROFILE` variable.

If you're using other shells, the process is similar, just replace `powershell` with your shell name and put the generated script in the appropriate place for your shell.

```{note}
Currently, the autocompletion feature in Regolith is very basic; it only provides the autocompletion for the subcommands. It doesn't provide autocompletion for the flags and arguments.
```
