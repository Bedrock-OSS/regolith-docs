# Performance Tips

This section is a collection of performance tips that you can find scattered across the Regolith documentation. If your project is starting to run slowly, consider applying some of these optimizations:

- **RAM Drive for Temporary Files:** Using the {ref}`tmp_dir<tmp-dir-user-config>` user setting can significantly improve the performance of filter execution when combined with a RAM drive. By moving the temporary directory into RAM, you eliminate disk I/O bottlenecks.
- **Symlink Export:** The {ref}`--symlink-export<symlink-export>` flag provides a great performance improvement by creating symbolic links instead of copying files. However, note that it won't work if your `tmp_dir` points to a different drive, as you cannot symlink across different drives.
- **Size-Time Check:** Regolith uses the size-time-check optimization by default, which speeds up exports on subsequent runs by only copying changed files. However, for continuous integration (CI) environments where everything runs from scratch and only once, it's better to disable this feature using the {ref}`--disable-size-time-check<disable-size-time-check>` flag.
- **Async Filters:** Grouping filters to run concurrently as {ref}`async filters<project-config-running-async-filers>` is a powerful way to speed up your project. Just be careful to manage the dependencies and execution order between your filters correctly.
- **Node Runtime Overrides:** You can potentially speed up execution for NodeJS filters by overriding the runtime to use {ref}`Bun or Deno<node-runner-override>` instead.