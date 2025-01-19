(testing-filters)=
# Testing Filters
The {ref}`Online Filters<online-filters>` page mentions the existence of a `test` folder. While Regolith doesn't provide a built-in testing framework, here's a recommended approach to set up and test your online filters effectively.

We suggest using the `test` folder as a dedicated space to store a testing Regolith project. This project should contain test cases that verify your filter's functionality. Follow these steps to set up your test environment:

**1.** Create a new Regolith project in the `test` folder by running:
```text
regolith init
```

**2.** Set the {ref}`export target<export-targets>` to `local`. This prevents Regolith from exporting files to the default `com.mojang` folder.

Here's the refined and formatted version of the "Testing Filters" section:

**3.** Add the `build` folder to your `.gitignore` file to keep unnecessary build artifacts out of your repository.

**4.** Install the [Filter Tester](https://github.com/Bedrock-OSS/regolith-filters/tree/master/filter_tester)  filter using:
```text
regolith install filter_tester
```

The Filter Tester verifies the Regolith output against a predefined set of expected results.

**5.** Define your online filter as a local filter in the project by referencing its script. You can use `..` in the path to point to the parent folder where the filter resides. For example:
```json
"filterDefinitions": {
    "example_filter": {
        "runWith": "python",
        "script": "../example.py"
    }
}
```
This configuration assumes the filter script is in the parent directory under the file `example.py`.

**6.** The Filter Tester can stop execution when the output of your filter doesn't match the expected results (see the [Filter Tester README](https://github.com/Bedrock-OSS/regolith-filters/tree/master/filter_tester#readme)).

This setting is useful when you want to setup CI on your repository. If you set the filter not to stop on error, you can run the tests and see the differences as errors in the console.

When writing the tests, simply add example inputs to your test project, run Regolith and check the output in the `build` folder. If the output matches the expectations, copy it to the `RP` and `BP` folders inside the data folder of the `filter_tester` filter.

```{note}
Refer to [this repository](https://github.com/Nusiq/regolith-filters/tree/master/system_template) for an example project that follows these steps.
```
