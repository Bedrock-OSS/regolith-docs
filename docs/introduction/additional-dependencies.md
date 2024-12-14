(additional-dependencies)=
# Additional Dependencies

Regolith can be used as a stand-alone tool for generating Minecraft packs with your local filters. However, you can get the most out of Regolith created by its community and published on the internet. To use these filters, you will need to install additional dependencies. The dependencies you need depend on your workflow. This secotion provides some recommendations/requirements for using Regolith with filters from the internet.

(git-dependency)=
## Git
Git is the most popular version control system in the world. It is also the most important dependency of Regolith. Without Git, you won't be able to install filters in your projects. Regolith uses Git to download filters from the internet repositories like GitHub.

You can download Git from its website: [https://git-scm.com/download/](https://git-scm.com/download/)

## Filter Runners

Regolith supports filters written in various programming languages. To run these filters, you will need to install the appropriate runtime. You can find the installation instruction for each runtime in pages dedicated to different filter types:
 - {ref}`Python<python-filters>`
 - {ref}`NodeJS<node-filters>`
 - {ref}`Deno<deno-filters>`
 - {ref}`Java<java-filters>`
 - {ref}`Nim<nim-filters>`
 - {ref}`.NET<dotnet-filters>`

The runtimes are optional, unless you want to use filters written in the corresponding language.