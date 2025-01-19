(troubleshooting)=
# Troubleshooting

Regolith is a useful tool, but its somewhat complex compilation flow leaves room for user error. This page will explain solutions to common mistakes, as well as guide you through more complex debugging strategies.

## General Debugging Tips

### Reading the Console

Regolith runs in a terminal, providing valuable output during its execution. If something goes wrong, the console logs will often contain warnings, errors, or other helpful details about the issue.

Familiarize yourself with the console output and look for keywords like "warning" or "error" to identify problems. Reading the log carefully is often the first step in diagnosing an issue.

### Checking Your Version

Regolith is a living, breathing application, which is receiving numerous updates. You can directly install the latest version of Regolith, or watch out for the "A new Version is Available" messages in the console output.

## Common Issues

### Regolith Command Not Recognized

If you see an error like this when trying to run Regolith:

```text
regolith : The term 'regolith' is not recognized as the name of a cmdlet, function, script file,
or operable program.

Check the spelling of the name, or if a path was included, verify that the path is correct and
try again.
```

The most common cause of this issue is incorrect installation. Here are some troubleshooting tips:

1. **Restart Your Terminal:** Close the terminal or shell you're using and reopen it. Then try running the `regolith` command again.
2. **Switch Terminals:** Try a different shell. For example `gitbash` or `vscode` instead of `powershell`.
3. **Try reinstalling Regolith.**
4. **Use the Stand-Alone Executable:** If you cannot get Regolith installed, you may download the stand-alone executable, and place it in your project

### Crash When Running

The most common reason Regolith will crash is from a broken filter. The first step in debugging, is identifying which filter is failing. You can do so by navigating to the Regolith output log, and finding which filter caused the crash.

Filter errors will be printed like `[error][filter] ... `.

Where `filter` will be replaced with the name of the filter that had an error.

### Dependency Not Found

If Regolith cannot find a required dependency, you'll see an error like:


```text
[+] ... not found, download and install it from ...
```

This means the filter you're trying to use depends on a runtime or library that is missing from your system.

Example errors:
- Python `[+]: Python not found, download and install it from https://www.python.org/downloads/`
- NodeJS `[+]: NodeJS not found, download and install it from https://nodejs.org/en/`
