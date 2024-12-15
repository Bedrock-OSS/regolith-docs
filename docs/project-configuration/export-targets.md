(export-targets)=
# Export Targets

Export Targets are defined in {ref}`profileds<profiles>` and determine where your generated files will go, after Regolith is finished compiling.

All of the export settings require using the `target` property. Some of the export targets require additional properties. Sections below lists all of the available export targets.

## Export Target Types
### Development Export Target

The development export target will place the compiled packs into your `com.mojang` `development_*_packs` folders of the specified Minecraft build - Bedrock Edition, Education Edition or Preview.

```json
"export": {
    "target": "development",
    "build": "standard",
    "rpName": "'my_rp'",
    "bpName": "'my_bp'"
}
```

Properties:
- `build` - The Minecraft Edition to export to. Can be `standard`, `preview` or `education`. You can fake the `com.mojang` path using {ref}`export target environment variables<export-target-environment-variables>`.
- `rpName` (optional) - The {ref}`go-simple-eval<go-simple-eval>` expression used to generate the name of the resource pack folder. If not specified, defaults to `"project.name+'_rp'"`.
- `bpName` (optional) - The {ref}`go-simple-eval<go-simple-eval>` expression used to generate the name of the behavior pack folder. If not specified, defaults to `"project.name+'_bp'"`.
 - `readOnly` (optional) - If set to `true`, the exported files will be read-only. The default value is `false`.

### Local Export Target

This export target will place the compiled packs into a folder called `build`, created in your regolith project. This export target is mostly useful for quick testing.

```json
"export": {
    "target": "local",
    "rpName": "'my_rp'",
    "bpName": "'my_bp'"
}
```

Properties:
- `rpName` (optional) - The {ref}`go-simple-eval<go-simple-eval>` expression used to generate the name of the resource pack folder. If not specified, defaults to `"project.name+'_rp'"`.
- `bpName` (optional) - The {ref}`go-simple-eval<go-simple-eval>` expression used to generate the name of the behavior pack folder. If not specified, defaults to `"project.name+'_bp'"`.
- `readOnly` (optional) - If set to `true`, the exported files will be read-only. The default value is `false`.

### None Export Target
The `none` export target runs Regolith without exporting the files anywhere. This is useful when you have a filter that exports the files in some other custom way.

```json
"export": {
    "target": "none"
}
```
The `none` doesn't have any additional properties.


### Exact Export Target

The Exact export target will place the files to specific, user specified locations. This is useful when you need absolute control over Regoliths export functionality.

```json
"export": {
    "target": "exact",
    "rpPath": "...",
    "bpPath": "..."
}
```

Properties:
- `rpPath` - The path to the resource pack folder. The path can be relative or absolute and supports environment variables by using the `%VARIABLE_NAME%` syntax.
- `bpPath` - The path to the behavior pack folder. The path can be relative or absolute and supports environment variables by using the `%VARIABLE_NAME%` syntax.
- `readOnly` (optional) - If set to `true`, the exported files will be read-only. The default value is `false`.

### World Export Target

The World export target will place the compiled files into a specific world. This is useful for teams that prefer working in-world, as opposed to in the development pack folders.

```json
"export": {
    "target": "world",
    "build": "standard",
    "worldName": "...",      // This
    // "worldPath": "...",   // OR this
    "rpName": "'my_rp'",
    "bpName": "'my_bp'"
}
```
There are two ways of using the `"world"` export target, by specifying the `worldName` or `worldPath` property.

Properties when using the world name:
- `build` - The Minecraft Edition to export to. Can be `standard`, `preview` or `education`. You can fake the `com.mojang` path using {ref}`export target environment variables<export-target-environment-variables>`.
- `worldName` - The name of the world to export to. Regolith uses the *levelname.txt* file stored in the world files to determine the name of the world.

Properties when using the world path:
- `worldPath` - The complete path to the world to export to. The path can be relative or absolute and supports environment variables by using the `%VARIABLE_NAME%` syntax.

Shared properties:
- `rpName` - The {ref}`go-simple-eval<go-simple-eval>` expression used to generate the name of the resource pack folder. If not specified, defaults to `"project.name+'_rp'"`.
- `bpName` - The {ref}`go-simple-eval<go-simple-eval>` expression used to generate the name of the behavior pack folder. If not specified, defaults to `"project.name+'_bp'"`.
- `readOnly` (optional) - If set to `true`, the exported files will be read-only. The default value is `false`.


(export-target-environment-variables)=
## Export Target Environment Variables

```{warning}
These environment variables are only available for non-Windows users.
```

Some of the export targets listed above wouldn't make sense on systems other than Windows with Minecraft installed. They often rely on finding the `com.mojang` path first, and then placing the files in a path relative to that. This problem can be solved by setting environment variables that Regolith will use instead of the `com.mojang` path.

- `COM_MOJANG` - A fake path to the `com.mojang` folder in regular Minecraft releases. This is used by the `development` build.
- `COM_MOJANG_PREVIEW` - A fake path to the `com.mojang` folder in Minecraft preview releases. This is used by the `preview` build.
- `COM_MOJANG_EDU` - A fake path to the `com.mojang` folder in Minecraft Education Edition releases. This is used by the `education` build.
