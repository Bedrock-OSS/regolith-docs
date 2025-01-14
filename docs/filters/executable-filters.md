(executable-filters)=
# Executable Filters

Executable filters allow the usage of compiled executable files. If you want to use a compiled programing language to develop your filters, this is the way to go. Executable filters don't require any additional runtime to be installed, however, you need to make sure that the executable is compiled for the platform you are running Regolith on.

## Executable Filter Definition

The the structure of the executable filter definition is described below. You can read how to use it in the {ref}`Filter Definition<filter-definition>` section.

```json
{
  "runWith": "exe",
  "exe": "path/to/your/executable.exe"
}
```

- `runWith` - always set to `exe`, marks this filter as a exe filter.
- `path` - path to the executable file. On Windows, the file extension should be `.exe`. On other platforms, the file extension is optional.

## Developing Executable Filters and Multiple Platforms

Since compiled programs are platform-specific using the on multiple platforms can be tricky. Luckily, Regolith got you covered. You can use the {ref}`when<project-config-when-property>` property to run programs conditionally based on the platform.

If you're writing an {ref}`online filter<online-filters>` you can use the `when` property in the `filters` list of the filter.json file. Example:
````json
"filters": [
  {
    "runWith": "exe",
    "exe": "coolThing.exe",
    "when": "os == 'windows'"
  },
  {
    "runWith": "exe",
    "exe": "coolThingLinux",
    "when": "os == 'linux'"
  },
  {
    "runWith": "exe",
    "exe": "coolThingMac",
    "when": "os == 'darwin'"
  }
]
````

If you're writing a {ref}`local filter<local-filters>` you can have to define a separate filter for each platform in `filterDefinitions` and then run them conditionally in the `filters` list of the {ref}`config.json<project-config-file>` file. Example:
```json
"filterDefinitions": {
  "cool_thing_windows": {
    "runWith": "exe",
    "exe": "filters/coolThing.exe"
  },
  "cool_thing_linux": {
    "runWith": "exe",
    "exe": "filters/coolThingLinux"
  },
  "cool_thing_osx": {
    "runWith": "exe",
    "exe": "filters/coolThingMac"
  }
},
"profiles": {
  "default": {
    "export": {
      "target": "development"
    },
    "filters": [
      {
        "filter": "cool_thing_windows",
        "when": "os == 'windows'"
      },
      {
        "filter": "cool_thing_linux",
        "when": "os == 'linux'"
      },
      {
        "filter": "cool_thing_osx",
        "when": "os == 'darwin'"
      }
    ]
  }
}
```


