(performance-options)=
# Performance Options

Regolith provides several options to control how files are exported, which can improve performance for large projects.

## Size-Time Check

By default, Regolith uses a size-time check optimization when exporting files. It compares the size and modification time of files before copying them between working and output directories. If the source file and the destination file have the same size and modification time, Regolith assumes they are identical and leaves the destination file unchanged.

The size-time check should greatly speed up the exports of large projects on subsequent runs.

The downside of this approach is that on the first run, the export will be slower, but on subsequent runs, the export will be much faster. This means that the size-time check is not recommended for CI where Regolith is run only once. This feature is also not recommended for projects where most of the files are generated on the fly, as the size and modification time will always be different.

If you want to disable this optimization (for example, in CI environments), use the `--disable-size-time-check` flag:

```
regolith run --disable-size-time-check
regolith watch --disable-size-time-check
```

## Symlink Export

The `--symlink-export` flag allows Regolith to use symbolic links when exporting files from the {ref}`working directory<the-working-directory-of-filters>` to the output directory. Instead of copying files, Regolith creates symlinks in the working directory that point to the files in the output directory. This can speed up the export process, especially for large projects with many files.

The downside of this approach is that Regolith deletes the contents of the output directory before generating files. This means that if generating fails, the output directory will be left empty or incomplete until the next successful run.

Usage:
```
regolith run --symlink-export
regolith watch --symlink-export
```

```{note}
When using this flag, Regolith will always create output RP and BP files in the output directory, even if they're empty. This is to ensure that the symlinks in the working directory always point to valid files.
```

## Combining Options

It's possible to combine `--symlink-export` and `--disable-size-time-check` flags. When both `--symlink-export` and the default size-time check are active, Regolith uses an optimized sync that leverages the benefits of both.
