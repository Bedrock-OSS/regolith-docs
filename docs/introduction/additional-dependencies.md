(additional-dependencies)=
# Additional Dependencies

Regolith can be used as a stand-alone tool for generating Minecraft packs with your local filters. However, you can get the most out of Regolith created by its community and published on the internet. To use these filters, you will need to install additional dependencies. The dependencies you need depend on your workflow. This secotion provides some recommendations/requirements for using Regolith with filters from the internet.

(git-dependency)=
## Git
Git is the most popular version control system in the world. It is also the most important dependency of Regolith. Without Git, you won't be able to install filters in your projects. Regolith uses Git to download filters from the internet repositories like GitHub.

You can download Git from its website: [https://git-scm.com/download/](https://git-scm.com/download/)

(nodejs-dependency)=
## NodeJS
NodeJS is a JavaScript runtime. It is also the most popular option for writing Regolith filters. If you're making Minecraft packs, there's a good chance you're already familiar with JavaScript, and have NodeJS installed.

You can download NodeJS here: [https://nodejs.org/en/download/package-manager](https://nodejs.org/en/download/package-manager)

```{note}
The [Gametests](https://github.com/Bedrock-OSS/regolith-filters/tree/master/gametests) filter is a very notable filter that for many users could be the main selling point of Regolith. Gametests is a filter that lets you use TypeScript. It compiles the script in the pack using ESBuild.

The unusual name of the filter is a relic of its time of creation. The filter was created before current Scripting API was released. At that time, Minecraft only had the "gametest" API designed for writing tests of the packs. The filter was named after this API.
```

(python-dependency)=
## Python
Python is the second most popular language for writing Regolith filters.

We provide detailed instructions on how to install Python in the {ref}`Python Filters<installing-python>` section.

## Other languages
Regolith supports many other languages, including writing shell scripts (which basically unlocks the ability to use any language). You can find instructions for installing these languages in the documentation for each filter type.
