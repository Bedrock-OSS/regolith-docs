# Experiments
Experiments are new experimental features of Regolith to be released in the future versions, once proven to be stable and useful. The experiments can be enabled with the `--experiments` flag.

## size_time_check
The `size_time_check` experiment aims to improve the performance of the `regolith run` and `regolith watch` commands. It does this by comparing the size and modification time of files before copying them between working and output directories. If the source file and the destination file have the same size and modification time, Regolith assumes they are identical and leaves the destination file unchanged.

The `size_time_check` should greatly speed up the exports of large projects.

The downside of this approach is that on the first run, the export will be slower, but on subsequent runs, the export will be much faster. This means that the `size_time_check` is not recommended for CI where Regolith is run only once. This feature is also not recommended for the projects where most of the files are generated on the fly, as the size and modification time will always be different.

Usage:
```
regolith run --experiments size_time_check
regolith watch --experiments size_time_check
```
