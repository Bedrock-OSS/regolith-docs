(format-versions)=
# Format Versions
This page lists changes in different format versions of the Regolith {ref}`config.json<project-config-file>` file.

- `1.2.0` - The first available `formatVersion`. This is the default if the field is not specified.
- `1.4.0` - This version changed the way the `export` field works. You can read about the current implementation of the export target in {ref}`it's own page<export-targets>`. Unfortunately, the `1.4.0` format change was implemented before we had versioned documentation, so the only way to read about it now is to look at the [source of the old version of the documentation](https://github.com/Bedrock-OSS/regolith/blob/1.2.0/docs/docs/guide/export-targets.md).

```{warning}
The `formatVersion` field was introduced quite late in the development of Regolith. The format version changes when the format of the configuration file changes in a way that breaks the backward compatibility. The format versions use the same version number as the version of Regolith that introduce them. Not all versions of Regolith add new format version. The lowest possible value and the default (if not specified) is `1.2.0`.
```