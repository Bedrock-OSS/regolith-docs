(format-versions)=
# Format Versions
This page outlines changes introduced in different `formatVersion` values for the Regolith {ref}`config.json<project-config-file>` file.

- `1.2.0`: The first available `formatVersion`. If the `formatVersion` field is not specified, this value is used as the default.
- `1.4.0`: This version introduced changes to the `export` field functionality. You can learn about the current implementation of export targets on {ref}`its dedicated page<export-targets>`.Unfortunately, the `1.4.0` format change was made before Regolith implemented versioned documentation. To review its previous behavior, you'll need to consult the [source of the old documentation](https://github.com/Bedrock-OSS/regolith/blob/1.2.0/docs/docs/guide/export-targets.md) .

```{warning}
The `formatVersion` field was introduced later in Regolith's development.

A new `formatVersion` is created whenever changes to the configuration file format break backward compatibility. The `formatVersion` values correspond to the version of Regolith that introduced them.

Not every version of Regolith introduces a new `formatVersion`. If this field is omitted from the `config.json` file, the lowest possible value, `1.2.0`, is used by default.
```