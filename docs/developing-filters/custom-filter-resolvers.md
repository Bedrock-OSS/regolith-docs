(custom-filter-resolvers)=
# Custom Filter Resolvers
```{warning}
This page explains filter resolvers from the perspective of a filter developer. For a basic understanding of what filter resolvers are and how to use them, refer to the {ref}`Filter Resolvers<filter-resolvers>` section.
```

Filter resolvers in Regolith, like filters, are stored in Git repositories. A filter resolver is a JSON file that lists filter names and their corresponding URLs.

## Structure of a Resolver File
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
Specifies the version of the resolver file format using [semantic versioning](https://semver.org/). The current version is `1.0.0`.

```{note}
Regolith currently ignores the `formatVersion` property entirely, but it's still recommended to include it for future compatibility.
```

### filters: object
Contains filter names and their corresponding repository URLs. Used to construct the full URL for the {ref}`regolith install<install-command>` command by combining `<filter-url>/<filter-name>`.

For example, with the resolver file above, added to your user configuration, running:
```text
regolith install filter_tester
```
would be equivalent to running: 
```text
regolith install github.com/Bedrock-OSS/regolith-filters/filter_tester
```

## Adding Custom Resolvers to User Configuration
To use a custom resolver, add its URL to your user configuration using the {ref}`regolith config<regolith-config-command>` command.

For example, to add a resolver from the `github.com/Bedrock-OSS/example` respotiory, that is defined in the `resolver.json` file, you would run:
```text
regolith config resolvers --append github.com/Bedrock-OSS/example/resolver.json
```

This command appends the custom resolver URL to your configuration, making its filters available for use.
