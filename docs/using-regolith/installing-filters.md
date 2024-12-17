(installing-filters)=
# Installing Filters

To start using a filter, you need to do four things:

 1. Ensure you can run the filter
 2. Install the filter
 3. Add the filter to the profile which you would like to use it.
 4. Run your profile, to test it out!

## Filter Dependencies

Filters are written in [programming languages](https://www.wikiwand.com/en/Programming_language). These languages may not be installed on your computer by default. Before installing a filter, you should ensure you have the proper programming language installed. The "Filter Types" documentation has detailed installation instructions for every regolith-supported language!

For example, if the filter relies on Python, you can find installation instructions {ref}`here<python-filters>`.

## Installing a Filter

Regolith contains a powerful installation command, which will download a filter from GitHub, and install any required libraries for you. In general, the format is like this: `regolith install <filter_identifier>`

The value of `filter_identifier` will depend on where the filter is hosted. Filters listed on the [Bedrock-OSS/regolith-filter-resolver](https://github.com/Bedrock-OSS/regolith-filter-resolver/blob/main/resolver.json) repository can be installed by their name. For example, to install the `name_ninja` filter, you would run the:

```
regolith install name_ninja
```
If the filter is not listed on the resolver repository, you will need to use the following format:
`github.com/<user>/<repository>/<folder>`.

For example, to install `name_ninja` using the full format, you would run:

```
regolith install github.com/Bedrock-OSS/regolith-filters/name_ninja
```
The longer form can be used to install filters from private repositories.


```{warning}
The `install` command relies on `git`. You may download git [here](https://git-scm.com/download/win).
```

## Adding Filter to Profile

After installing, the filter will appear inside of `filter_definitions` of `config.json`. You can now add this filter to a profile like this:

```json
"default": {
  "export": {
    "readOnly": false,
    "target": "development",
    "build": "standard"
  },
  "filters": [
    {
      "filter": "FILTER_NAME",
    }
  ]
}
```

## Install All

Regolith is intended to be used with git version control, and by default the `.regolith` folder is ignored. That means that when you collaborate on a project, or simply re-clone your existing projects, you will need an easy way to download all the filters again!

You may use the command `regolith install-all`, which will check `config.json`, and install every filter in the `filterDefinitions`.

```{warning}
This is only intended to be used with existing projects. To install new filters, use `regolith install`.
```
