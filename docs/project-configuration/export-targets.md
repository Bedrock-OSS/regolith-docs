(export-targets)=
# Export Targets
Export Targets are defined in {ref}`profileds<profiles>` and determine where your generated files will go, after Regolith is finished compiling.

All export settings require the `target` property. Some export targets may require additional properties, which are detailed in the sections below.

## Export Target Types
### Development Export Target
The `development` export target places compiled packs into the `com.mojang` `development_*_packs` folders for the specified Minecraft build - Bedrock Edition, Education Edition, or Preview.

```json
"export": {
    "target": "development",
    "build": "standard",
    "rpName": "'my_rp'",
    "bpName": "'my_bp'"
}
```
Properties:
- `build`: Specifies the Minecraft edition to export to. Options are:
  - `standard` (Minecraft Bedrock Edition)
  - `preview` (Minecraft Preview)
  - `education` (Minecraft Education Edition)

  You can simulate the `com.mojang` path using {ref}`export target environment variables<export-target-environment-variables>`.
- `rpName` (optional): A {ref}`go-simple-eval<go-simple-eval>` expression that generates the name of the resource pack folder. Defaults to `"project.name+'_rp'"` if not specified.
- `bpName` (optional): A {ref}`go-simple-eval<go-simple-eval>` expression that generates the name of the behavior pack folder. Defaults to `"project.name+'_bp'"` if not specified.
- `readOnly` (optional): If set to `true`, the exported files will be read-only. Defaults to `false`.

### Local Export Target
The `local` export target  places compiled packs into a `build` folder within your Regolith project directory. This target is ideal for quick testing.

```json
"export": {
    "target": "local",
    "rpName": "'my_rp'",
    "bpName": "'my_bp'"
}
```

Properties:
- `rpName` (optional): A {ref}`go-simple-eval<go-simple-eval>` expression that generates the name of the resource pack folder. Defaults to `"project.name+'_rp'"` if not specified.
- `bpName` (optional): A {ref}`go-simple-eval<go-simple-eval>` expression that generates the name of the behavior pack folder. Defaults to `"project.name+'_bp'"` if not specified.
- `readOnly` (optional): If set to `true`, the exported files will be read-only. Defaults to `false`.

### None Export Target
The `none` export target runs Regolith without exporting files. This option is useful if your filters handle file export in a custom way.

```json
"export": {
    "target": "none"
}
```
The `none` doesn't have any additional properties.

### Exact Export Target
The `exact` export target  allows you to specify the exact locations for the exported files. This target provides full control over the export functionality of Regolith.

```json
"export": {
    "target": "exact",
    "rpPath": "...",
    "bpPath": "..."
}
```

Properties:
- `rpPath`: The path to the resource pack folder. The path can be relative or absolute and supports environment variables using the `%VARIABLE_NAME%` syntax.
- `bpPath`: The path to the behavior pack folder. The path can be relative or absolute and supports environment variables using the `%VARIABLE_NAME%` syntax.
- `readOnly` (optional): If set to `true`, the exported files will be read-only. Defaults to `false`.

### World Export Target
The `world` export target places the compiled files into a specific world, making it ideal for teams who prefer working directly within the world rather than in development pack folders.

```json
"export": {
    "target": "world",
    "build": "standard",
    "worldName": "...",      // Use this
    // "worldPath": "...",   // OR this
    "rpName": "'my_rp'",
    "bpName": "'my_bp'"
}
```
There are two ways to use the `"world"` export target:
1. By specifying the `worldName`
2. By specifying the `worldPath`

Properties when using `worldName`:
- `build`: The Minecraft edition to export to. Can be `standard`, `preview`, or `education`. You can simulate the `com.mojang` path using {ref}`export target environment variables<export-target-environment-variables>`.
- `worldName`: The name of the world to export to. Regolith uses the *levelname.txt* file stored in the world folder to determine the world name.

Properties when using `worldPath`:
- `worldPath`: The complete path to the world to export to. The path can be relative or absolute and supports environment variables using the `%VARIABLE_NAME%` syntax.

Shared Properties (for both options):
- `rpName` (optional): A {ref}`go-simple-eval<go-simple-eval>` expression to generate the name of the resource pack folder. Defaults to `"project.name+'_rp'"` if not specified.
- `bpName` (optional): A {ref}`go-simple-eval<go-simple-eval>` expression to generate the name of the behavior pack folder. Defaults to `"project.name+'_bp'"` if not specified.
- `readOnly` (optional): If set to `true`, the exported files will be read-only. Defaults to `false`.

(export-target-environment-variables)=
## Export Target Environment Variables

Some of the export targets listed above wouldn't make sense on systems other than Windows with Minecraft installed. They often rely on finding the `com.mojang` path first, and then placing the files in a path relative to that. This problem can be solved by setting environment variables that Regolith will use instead of the `com.mojang` path.

- `COM_MOJANG`: A fake path to the `com.mojang` folder in regular Minecraft releases. Used by the `development` build.
- `COM_MOJANG_PREVIEW`: A fake path to the `com.mojang` folder in Minecraft preview releases. Used by the `preview` build.
- `COM_MOJANG_EDU`: A fake path to the `com.mojang` folder in Minecraft Education Edition releases. Used by the `education` build.

Starting with Regolith 1.5.2, environment variables can be used on Windows as well. These variables take precedence over the default com.mojang paths.
