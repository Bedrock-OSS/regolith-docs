(publishing-filters)=
# Publishing Filters

If you create an {ref}`online filter<online-filters>` and upload it to a public repository on any Git hosting service, it will already be available for anyone who knows the URL via the {ref}`regolith install<install-command>` command.

However, if you want to make your filter discoverable by Regolith users, you should consider adding it to the {ref}`default filter resolver<default-filter-resolver>`.

For GitHub users, the process is straightforward. Simply add a [regolith-filter](https://github.com/topics/regolith-filter) topic to your repository. You can learn how to add topics on the official [GitHub documentation](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/classifying-your-repository-with-topics#adding-topics-to-your-repository).

```{note}
The filters aren't added to the default resolver instantly. The resolver is updated periodically, using a GitHub Action that runs every 24 hours.
```

If you are using a different Git hosting service, there is no automatic way to add your filter to the default resolver. You can contact the Regolith team on our [Discord server](https://discord.gg/UQ82Qrean7) to add your filter to the [resolver repository](https://github.com/Bedrock-OSS/regolith-filter-resolver) manually.


