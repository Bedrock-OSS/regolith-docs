(publishing-filters)=
# Publishing Filters
Creating an {ref}`online filter<online-filters>` and uploading it to a public repository on any Git hosting service instantly makes it available for installation using the {ref}`regolith install<install-command>` command, provided users know the repository URL.

## Adding Filters to the Default Resolver
To make your filter easily discoverable by Regolith users, you can add it to the {ref}`default filter resolver<default-filter-resolver>`.

The process is straightforward. All you need to do is create a pull request to the [resolver repository](https://github.com/Bedrock-OSS/regolith-filter-resolver) and add the URL to your filter's repository to the `repos.json` file.

The structure is very simple, it's a JSON file with a list of known repositories:
```json
{
    "known_repos": [
        // Add your repository URL here.
    ]
}
```
You can also contact the Regolith team on our [Discord server](https://discord.gg/UQ82Qrean7) and ask to add your repository for you.

The default resolver repository runs a GitHub Action every 24 hours to add new filters from the `known_repos` to the resolver. Note that one repository can have multiple filters, so if it's added to the list once, you can publish as many filters as you want without going through the process again.

## The regolith-filter Topic
To help users discover your filters on GitHub, add the `regolith-filter` topic to your repository. This makes your filter searchable using this URL: [https://github.com/topics/regolith-filter](https://github.com/topics/regolith-filter).

Previously, this topic was used to automatically add filters to the default resolver, but this is no longer the case.

```{note}
For more information on adding topics to your GitHub repository, refer to the official [GitHub documentation](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/classifying-your-repository-with-topics#adding-topics-to-your-repository).
```
