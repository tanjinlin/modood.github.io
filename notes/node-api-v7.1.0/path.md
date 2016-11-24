# path

```
┌─────────────────────┬────────────┐
│          dir        │    base    │
├──────┬              ├──────┬─────┤
│ root │              │ name │ ext │
"  /    home/user/dir / file  .txt "
└──────┴──────────────┴──────┴─────┘
```

*   平台差异

    ```
    path.posix
    path.win32

    path.delimiter
    path.sep
    ```

*   文件路径

    ```
    path.dirname(path)
    path.basename(path[, ext])
    path.extname(path)

    path.format(pathObject)
    path.parse(path)

    path.isAbsolute(path)

    path.resolve([...paths])
    path.relative(from, to)

    path.join([...paths])
    path.normalize(path)
    ```

