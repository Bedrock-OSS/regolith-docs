(deno-filters)=
# Deno Filters

Deno filters can run scripts written in TypeScript or JavaScript for the Deno runtime as filters. Deno filters aren't compiled and may have additional dependencies that Regolith will download for you during `regolith install` execution.

## Installing Deno

Before you can run Deno filters, you will need to [install Deno](https://deno.land/).

## Deno Filter Definition

The the structure of the Deno filter definition is described below. You can read how to use it in the {ref}`Filter Definition<filter-definition>` section.

```json
{
  "runWith": "deno",
  "script": "./filters/example.ts"
}
```

- `runWith` - always set to `deno`, marks this filter as a Deno filter.
- `path` - path to the `.ts` or `.js` file that contains the main script of the filter to run.

## Requirements and Dependencies

The dependencies of a Deno filter are managed by the Deno runtime, they are specified in `deno.json`, `deno.jsonc` or `package.json` (depending on your project setup). To learn more about managing dependencies in Deno projects, refer to the Deno documentation. The Deno filters expect the dependencies to be specified in a configuration file located in the same directory as the script file.
