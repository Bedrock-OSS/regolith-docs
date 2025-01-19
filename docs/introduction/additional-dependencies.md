(additional-dependencies)=
# Additional Dependencies

Regolith can function as a stand-alone tool for generating Minecraft packs with your local filters. However, to fully leverage the power of Regolith and access filters shared online, additional dependencies may be required. These dependencies depend on your workflow. This section provides recommendations and requirements for using Regolith filters from the internet.

(git-dependency)=
## Git
Git is the most widely used version control system in the world and an essential dependency for Regolith. Without Git, you won't be able to install filters from online repositories, such as GitHub. Regolith relies on Git to download filters for your projects.

You can download Git from its official website:
[https://git-scm.com/download/](https://git-scm.com/download/)

## Filter Runners

Regolith supports filters written in various programming languages. To use these filters, you need to install the appropriate runtime environment. Installation instructions for each runtime can be found on the pages dedicated to specific filter types:
- {ref}`Python<python-filters>`
- {ref}`NodeJS<node-filters>`
- {ref}`Deno<deno-filters>`
- {ref}`Java<java-filters>`
- {ref}`Nim<nim-filters>`
- {ref}`.NET<dotnet-filters>`

These runtimes are optional unless you intend to use filters written in the corresponding languages. Some filter types do not require a runtime

- {ref}`Shell Filters<shell-filters>` run shell commands directly.
- {ref}`Executable Filters<executable-filters>` use precompiled executables.
