(node-filters)=
# NodeJS Filters

NodeJS is a JavaScript runtime. It is also the most popular option for writing Regolith filters. If you're making Minecraft packs, there's a good chance you're already familiar with JavaScript, and have NodeJS installed.

You can download NodeJS here: [https://nodejs.org/en/download/package-manager](https://nodejs.org/en/download/package-manager)

```{note}
The [Gametests](https://github.com/Bedrock-OSS/regolith-filters/tree/master/gametests) filter is a very notable filter that for many users could be the main selling point of Regolith. Gametests is a filter that lets you use TypeScript. It compiles the script in the pack using ESBuild.

The unusual name of the filter is a relic of its time of creation. The filter was created before current Scripting API was released. At that time, Minecraft only had the "gametest" API designed for writing tests of the packs. The filter was named after this API.
```

## Installing NodeJS

Before you can run Node filters, you will need to [install NodeJS](https://nodejs.org/en/download/).

## Running NodeJS code as Filter

The syntax for running a nodejs filter is this:

```json
{
  "runWith": "nodejs",
  "script": "./filters/example.js",

  // Optional property that defines the path to the folder with the package.json file
  "requirements": "./filters"
}
```

## Requirements and Dependencies

When installing, regolith will check for a `package.json` file. If requirements property is specified
reqolith will look in that folder, otherwise it will look in the folder with the script.

When developing a Node filter with dependencies, you must create this file. You can create a `package.json` file yourself by using `npm init`.
