(java-filters)=
# Java Filters

Java filters run compiled Java programs (`.jar` files) as filters, using the `java` command.

## Installing Java

Before you can run Java filters, you will need to install Java Development Kit.

There are many available JDKs to choose from. Few recommended are:
 - [OpenJDK](https://jdk.java.net/)
 - [AdoptOpenJDK](https://adoptopenjdk.net/)
 - [LibericaJDK](https://bell-sw.com/pages/downloads/)

## Java Filter Definition

The the structure of the Java filter definition is described below. You can read how to use it in the {ref}`Filter Definition<filter-definition>` section.

```json
{
  "runWith": "java",
  "path": "./filters/example.jar"
}
```

- `runWith` - always set to `java`, marks this filter as a Java filter.
- `path` - path to the `.jar` file that contains the compiled Java program to run.
