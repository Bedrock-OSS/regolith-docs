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
- `rpPath`: The path to the resource pack folder.
- `bpPath`: The path to the behavior pack folder.
- `readOnly` (optional): If set to `true`, the exported files will be read-only. Defaults to `false`.

The `rpPath` and `bpPath` can be relative or absolute and supports environment variables using the `%VARIABLE_NAME%`, `$VARIABLE_NAME` and `${VARIABLE_NAME}` syntax.

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


(how-does-regolith-determine-the-com-mojang-path)=
## How does Regolith determine the com.mojang path?

On Windows, Regolith uses default paths for Minecraft 1.21.120+.

For the standard build (Minecraft Bedrock):
- `development` exports go to `%APPDATA%/Minecraft Bedrock/Users/Shared/games/com.mojang/...` to development behavior and resource pack folders.
- `world` exports go to `%APPDATA%/Minecraft Bedrock/Users/<user-id>/games/com.mojang/` to the worlds folder, where `<user-id>` is the first found folder that isn't named `Shared`.

For the preview build (Minecraft Bedrock Preview), the structure is similar:
- `development`: `%APPDATA%/Minecraft Bedrock Preview/Users/Shared/games/com.mojang/...`
- `world`: `%APPDATA%/Minecraft Bedrock Preview/Users/<user-id>/games/com.mojang/...`

For the education build (Minecraft Education Edition), it defaults to `%APPDATA%/Minecraft Education Edition/games/com.mojang` for both `development` and `world` exports (no Users/Shared distinction).

On other operating systems, Regolith relies exclusively on {ref}`export target environment variables<export-target-environment-variables>`.

Environment variables always take precedence over defaults.

(export-target-environment-variables)=
## Export Target Environment Variables

Some export targets rely on the `com.mojang` path. Environment variables provide flexibility for overrides on non-Windows systems, testing without Minecraft, or custom configurations. You can choose any combination - more specific variables offer greater control over paths used for packs or worlds. Regolith prioritizes specific variables, then general ones.

When the variables are unset, Regolith uses the paths described in {ref}`How does Regolith determine the com.mojang path?<how-does-regolith-determine-the-com-mojang-path>`.

General variables:
- `COM_MOJANG`: Sets the `com.mojang` path for standard Minecraft (`development` and `world` exports).
- `COM_MOJANG_PREVIEW`: For Minecraft Preview (`preview` exports).
- `COM_MOJANG_EDU`: For Minecraft Education Edition (`education` exports).

More specific variables:
- `COM_MOJANG_WORLDS`: Sets the `com.mojang` path specifically for `world` exports in standard builds.
- `COM_MOJANG_PACKS`: For `development` exports in standard builds.
- `COM_MOJANG_WORLDS_PREVIEW`: For `world` exports in preview builds.
- `COM_MOJANG_PACKS_PREVIEW`: For `development` exports in preview builds.

Education edition doesn't have specific variables since its file structure contains only one `com.mojang` path.
