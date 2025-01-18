(testing-filters)=
# Testing Filters

The {ref}`Online Filters<online-filters>` page mentions the existence of a `test` folder. While Regolith doesn't have a built-in testing framework, we have some recommendations on how to set up tests for your online filters.

We recommend using the `test` folder as a place to store a testing Regolith project. The project should contain a set of test cases that you can run to verify that your filter works as expected. Here is a step-by-step guide on everything you need to do:


**1.** Initialize a new Regolith project in the test folder using:
```text
regolith init
```

**2.** Set the {ref}`export target<export-targets>` to `local`. This will prevent Regolith from exporting the files to your `com.mojang` folder which is the default behavior.

**3.** Add the `build` folder to the `.gitignore`. It's not needed in the repository and it's better to keep it clean.

**4.** Install the [Filter Tester](https://github.com/Bedrock-OSS/regolith-filters/tree/master/filter_tester) filter:
```
regolith install filter_tester
```
Filter tester is a filter that verifies the Regolith output against a set of expected results. 

**5.** Add your online filter to the project as a local filter. You can use `..` in the path to reference the the parent folder. For example:
```json
"filterDefinitions": {
    "example_filter": {
        "runWith": "python",
        "script": "../example.py"
    }
},
```
The definition above assumes that the filter script is in the parent folder of the project in the file `example.py`.

**6.** Filter Tester has a feature that lets you stop the execution when the output of the filter doesn't match the expected output (see the [README file of the filter](https://github.com/Bedrock-OSS/regolith-filters/tree/master/filter_tester#readme)). This setting is useful when you want to setup CI on your repository. If you set the filter not to stop on error, you can run the tests and see the differences as errors in the console.

When writing the tests, simply add example inputs to your test project, run Regolith and check the output in the `build` folder. If the output matches the expectations, copy it to the `RP` and `BP` folders inside the data folder of the `filter_tester` filter.

```{note}
You can use [this respository](https://github.com/Nusiq/regolith-filters/tree/master/system_template) as an example that follows the steps above.
```
