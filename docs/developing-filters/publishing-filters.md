(publishing-filters)=
# Publishing Filters

If you create an {ref}`online filter<online-filters>` and upload it to a public repository on any Git hosting service, it will already be available via the {ref}`regolith install<install-command>` command for anyone who knows the URL.

## Adding Filters to the Default Resolver

If you want to make your filter discoverable by Regolith users, you should consider adding it to the {ref}`default filter resolver<default-filter-resolver>`.

If the process is straightforward. All you need to do is create a pull request to the [resolver repository](https://github.com/Bedrock-OSS/regolith-filter-resolver) and add the URL to your filter's repository to the `repos.json` file.

The structure is very simple, it's a JSON file with a list of known repositories:
```json
{
    "known_repos": [
        // Put your repository URL here.
    ]
}
```
You can also just contact the Regolith team on our [Discord server](https://discord.gg/UQ82Qrean7) and ask to add it for you.

The default resolver respository runs a GitHub Action every 24 hours to add new filters from the `known_repos` to the resolver. Note that one repository can have multiple filters, so if it's added to the list once, you can publish as many filters as you want without going through the process again.

## The regolith-filter Topic

There is a convention that can help users find your filters on GitHub. You can add a `regolith-filter` topic to your repository. This way, users can search for filters using the this URL: [https://github.com/topics/regolith-filter](https://github.com/topics/regolith-filter)

The topic used to be used to add filters to the default resolver automatically, but this is no longer the case.

```{note}
You can learn how to add topics to your repositories on the official [GitHub documentation](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/classifying-your-repository-with-topics#adding-topics-to-your-repository).
```



