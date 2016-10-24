# Bash 中如何判断是否存在某个命令

Bash 提供了一些内建命令如 hash、type、command 能达到要求：

```
$ command -v foo >/dev/null 2>&1 || { echo >&2 "I require foo but it's not installed.  Aborting."; exit 1; }
$ type foo >/dev/null 2>&1 || { echo >&2 "I require foo but it's not installed.  Aborting."; exit 1; }
$ hash foo 2>/dev/null || { echo >&2 "I require foo but it's not installed.  Aborting."; exit 1; }
```

## 参考资料

* [Shell(Bash)中如何判断是否存在某个命令](https://segmentfault.com/q/1010000000156870)
* [Check if a program exists from a Bash script](http://stackoverflow.com/questions/592620/check-if-a-program-exists-from-a-bash-script)
