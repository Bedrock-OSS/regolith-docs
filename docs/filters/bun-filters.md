(bun-filters)=
# Bun Filters

Bun filters can run scripts written in JavaScript or TypeScript for the Bun runtime as filters.

```{note}
If you're a filter developer, it's recommended to publish filters as NodeJS filters unless your filter uses Bun-specific features. Users can use the {ref}`node_runner_override<node-runner-override>` configuration setting to run NodeJS filters with Bun, making them portable across runtimes.
```

## Installing Bun

Before you can run Bun filters, you will need to [install Bun](https://bun.com/).

## Bun Filter Definition

The structure of the Bun filter definition is described below. You can read how to use it in the {ref}`Filter Definition<filter-definition>` section.

```json
{
  "runWith": "bun",
  "script": "./filters/example.ts"
}
```

- `runWith` - always set to `bun`, marks this filter as a Bun filter.
- `script` - path to the `.js` or `.ts` file that contains the JavaScript/TypeScript program to run.

## Requirements and Dependencies

The dependencies of a Bun filter are defined in a `package.json` file. When a `package.json` file is found in the same directory as the script, Regolith automatically runs `bun install` during `regolith install` to install the dependencies.
