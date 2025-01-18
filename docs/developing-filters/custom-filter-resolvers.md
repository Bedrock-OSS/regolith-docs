(custom-filter-resolvers)=
# Custom Filter Resolvers

```{warning}
This page describes the use of the filter resolvers from the filter developer's perspective. If you are looking for a basic explanation of what filter resolvers are, and how to use them, see the {ref}`Filter Resolvers<filter-resolvers>` section.
```

Filter resolvers, just like filters in Regolith are stored in Git repositories. Filter resolver is a single JSON file that contains a list of names of the filters and their URLs.

## Structure of Resolver File
```json
{
  "formatVersion": "1.0.0",
  "filters": {
    "filter_tester": {
      "url": "github.com/Bedrock-OSS/regolith-filters"
    },
    "gametests": {
      "url": "github.com/Bedrock-OSS/regolith-filters"
    }
  }
}
```

### formatVersion: string
The `formatVersion` property is a string with semver that defines the version of the resolver file format. The current version is `1.0.0`.

```{note}
The default resolver repository is using the `1.1.0` format version and includes some additional properties. These properties may be used by Regolith in the future, but for now, they are ignored.

In fact, Regolith currently ignores the `formatVersion` property entirely, but it's still recommended to include it for future compatibility.
```

### filters: object

The `filters` property is an object that contains the names of the filters and URLs to their repositories. Together they are used to create a "URL" for the {ref}`regolith install<install-command>` command by combining `<filter-url>/<filter-name>`.

For example, with the resolver file above, added to your user configuration, running:
```text
regolith install filter_tester
```
would be equivalent to running: 
```text
regolith install github.com/Bedrock-OSS/regolith-filters/filter_tester
```

## Adding Custom Resolvers to User Configuration

You can add the URL of your custom resolver to your user configuration using the {ref}`regolith config<regolith-config-command>` command.

For example, to add a resolver from the `github.com/Bedrock-OSS/example` respotiory, that is defined in the `resolver.json` file, you would run:

```text
regolith config resolvers --append github.com/Bedrock-OSS/example/resolver.json
```
