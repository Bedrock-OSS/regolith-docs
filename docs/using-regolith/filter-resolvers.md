(filter-resolvers)=
# Filter Resolvers

```{warning}
This section only describes the resolvers from the user's perspective. If you are a filter developer and you want to know the details of creating your own resolver repository, see the {ref}`Custom Filter Resolvers<custom-filter-resolvers>` section.
```

Filter resolvers are files hosted on the internet that Regolith can use to resolve the short names of the filters to their full URLs when running the `regolith install` command.

Thanks to this feature, you can run:
```text
regolith install name_ninja
```
And you don't have to remember the full URL of the filter and write commands like:
```text
regolith install github.com/Bedrock-OSS/regolith-filters/name_ninja
```

## Default Resolver
By default, Regolith uses the default resolver hosted at [Bedrock-OSS/regolith-filter-resolver](https://github.com/Bedrock-OSS/regolith-filter-resolver) repository in the `resolver.json` file.

Currently, there is no way to remove the default resolver from Regolith, but you can add your own resolvers which will take precedence over the default resolver (see the next section).

## Adding Resolvers to Your User Configuration
The list of resolvers used by Regolith is stored in the {ref}`user configuration<user-configuration>` file. You can edit it manually or use the `regolith config`.

To add a resolver to the list, use `regolith config resolvers <resolver-path> --append`, where the `<resolver-path>` is the URL to the resolver repository, with the path to the resolver file relative to the root of the repository separated by a `/`.

For example:
```text
regolith config resolvers github.com/Example/example-repository/path/to/resolver.json --append
```
This command would append the `path/to/resolver.json` file from the `github.com/Example/example-repository` repository to the list of resolvers.

```{warning}
The "URLs" in the resolvers list are not actual URLs, but Regolith can uderstand that which part of the path is the repository URL and which part is the path to the resolver file.
```
You can also edit the {ref}`user configuration<user-configuration>` file manually.

## Removing Resolvers
To remove a resolver from the list, use the `--delete` flag combined with the `--index` flag to specify the index of the resolver you want to remove.

For example:
```text
regolith config resolvers --delete --index=0
```
This command would remove the first resolver from the list (indexing starts from 0).

If you don't specify the `--index` flag, all of the resolvers will be reomved.

If you don't know what resolvers are in the list you can always print them with the `regolith config resolvers` command.
