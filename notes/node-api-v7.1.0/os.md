# os

```
os.EOL                    定义了操作系统的 End-of-line 的常量
os.constants              包含了操作系统的常用常量，包括错误码和进程信号量等

os.hostname()             返回操作系统的主机名
os.type()                 返回操作系统名
os.platform()             返回操作系统平台名称，等同于 `process.platform`
os.release()              返回操作系统的发行版本
os.endianness()           返回 CPU 的字节序，可能的是 "BE" 或 "LE"
os.arch()                 返回操作系统 CPU 架构，可能的值有 "x64"、"arm" 和 "ia32"。等同于 `process.arch`
os.cpus()                 返回一个对象数组，包含所安装的每个 CPU/内核的信息：型号、速度、时间。
os.networkInterfaces()    返回网络接口列表
os.loadavg()              返回一个包含 1、5、15 分钟平均负载的数组
os.totalmem()             返回操作系统内存总量
os.freemem()              返回操作系统空闲内存量
os.userInfo([options])    返回当前用户信息
os.homedir()              返回当前用户宿主目录
os.tmpdir()               返回操作系统的默认临时文件夹
os.uptime()               返回操作系统运行的时间
```

