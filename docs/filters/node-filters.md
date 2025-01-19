(node-filters)=
# NodeJS Filters

NodeJS filters run JavaScript code using NodeJS.

NodeJS is a JavaScript runtime. It is also the most popular option for writing Regolith filters. If you're making Minecraft packs, there's a good chance you're already familiar with JavaScript, and have NodeJS installed.

```{note}
The [Gametests](https://github.com/Bedrock-OSS/regolith-filters/tree/master/gametests) filter is a very notable filter that for many users could be the main selling point of Regolith. Gametests is a filter that lets you use TypeScript to develop your Minecraft packs. It transpiles the TypeScript code in your behavior pack to JavaScript using ESBuild.

The unusual name of the filter is a relic of its time of creation. The filter was created before current Scripting API was released. At that time, Minecraft only had the "gametest" API designed for writing tests of the packs. The filter was named after this API.
```

## Installing NodeJS

Before you can run NodeJS filters, you will need to [install NodeJS](https://nodejs.org/en/download/).

## NodeJS Filter Definition

The structure of the NodeJS filter definition is described below. You can read how to use it in the {ref}`Filter Definition<filter-definition>` section.

```json
{
  "runWith": "nodejs",
  "script": "./filters/example.js",
  "requirements": "./filters"
}
```

- `runWith` - always set to `nodejs`, marks this filter as a NodeJS filter.
- `script` - path to the `.js` file that contains the JavaScript program to run.
- `requirements` (optional) - a property that defines the path to the folder with the `package.json` file. By default, Regolith looks for the `package.json` file in the same folder as the script.


## Requirements and Dependencies

The dependencies of a NodeJS filter are defined in a `package.json` file. You can read more about the `package.json` file in the NodeJS documentation. The NodeJS filters expect the dependencies to be installed in the `package.json` file located in the same directory as the script file unless specified otherwise in the `requirements` property.

When developing a NodeJS filter with dependencies, you must create `package.json`. You can create it by using `npm init`.
