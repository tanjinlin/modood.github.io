# 基础

## 常用功能

### 避免 sudo 输入密码

-   运行：

    `sudo visudo`

-   在尾部增加：

    ```
    # 属于 mwn 组的用户运行 sudo 不需要密码
    %mwn ALL=(ALL:ALL) NOPASSWD: ALL
    ```

### 进程和端口

-   查特定程序的进程号

    `pgrep redis`

    `ps -e | grep redis`

-   根据端口号查进程

    `netstat -lnp  | grep 8080`

    `lsof -Pnl +M -i4 | grep 8080`

    `fuser -un tcp 8080`

    [详细资料](http://www.linuxidc.com/Linux/2012-09/69684.htm)

### 让命令运行在后台

-   方法一

    `nohup <cmd> &`

-   方法二

    将一个或多个命名包含在“()”中就能让这些命令在子 shell 中运行中

    当我们将"&"也放入“()”内之后，我们就会发现所提交的作业并不在作业列表中，无法通过jobs来查看

    `(ping www.ibm.com &)`

## 常用命令

### 硬件资源相关

```
iostat                IO性能状态数据
free                  显示系统使用和空闲的内存情况，包括物理内存、交互区内存(swap)和内核缓冲区内存)
df                    报告文件系统磁盘空间的使用情况
quota                 显示磁盘已使用的空间与限制
quotaoff              用来关闭用户的磁盘空间的限制
quotaon               用来开启用户的磁盘空间的限制
mount                 加载指定的文件系统
umount                卸除文件系统
```

### 网络通信相关

```
ping                  使用 ICMP 协议的强制回显请求数据报以使主机或网关发送一份 ICMP 的回显应答
ifconfig              一个用来查看、配置、启用或禁用网络接口的工具
netstat               显示网络连接，路由表，接口状态，伪装连接，网络链路信息和组播成员组
nslookup              用于查找域名服务器的程序
traceroute            追踪网络数据包的路由途径
```

### 系统和进程相关

```
uname                 输出一组系统信息
shutdown              以一种安全的方式关闭系统
reboot                重启
ps                    查看进程状态
top                   显示当前系统正在执行的进程的相关信息，包括进程ID、内存占用率、CPU占用率等
kill                  发送指定的信号到相应进程
killall               发送一条信号给所有运行任意指定命令的进程
```

### Shell 相关

```
chsh                  用于改变用户的登录shell
watch                 用于周期性执行命令/定时执行命令
crontab               定时执行操作命令，每一个用户拥有自己的crontab，配置文件存在/var下面，不能被直接编辑
sleep                 暂停指定的秒数
suspend               暂停shell的执行
alias                 设置命令的别名
unalias               删除别名
bind                  显示或设置键盘按键与其相关的功能
clear                 清除终端屏幕，在终端中通过快捷键 Ctrl+L 清除屏幕
```
```
declare               与set命令功能一样，对shell环境变量进行显示、设置
export                显示和设置环境变量值
set                   设置shell
unset                 删除变量或函数
setenv                用于显示和设置环境变量
```

### 用户相关

```
useradd               新建用户
passwd                修改用户密码
finger                用户查看用户信息
login                 使用户放弃现在的使用的身份，重新登录系统
logout                用户退出系统，其功能和login命令对应
su                    切换用户
sudo                  通过su切换到root用户运行命令
write                 用于用户之间发送信息
wall                  将讯息传给每一个 mesg 设定为 yes 的上线使用者
```

### 文件相关

文件类型
```
-                     一般文件（ordinary file）：文本文件、二进制文件
d                     目录文件（directory）

b                     块设备文件
c                     字符设备文件
p                     管道设备
l                     符号链接文件（symbolic links）
```

文件处理
```
ls                    显示文件信息
cd                    切换目录
pwd                   输出当前工作目录
touch                 新建文件
mkdir                 新建目录
cp                    复制
mv                    移动／重命名
rm                    移除
cat                   查看文件内容
more                  查看文件内容
head                  查看文件内容
tail                  查看文件内容
ln                    在文件之间建立连接
diff                  比较两个文件的内容
diffstat              根据diff的比较结果，显示统计数字
file                  确定文件类型
whereis               定位可执行文件
```

权限管理
```
chmod                 文件文件的权限
chown                 修改文件的所有者和/或所属组
chgrp                 修改文件所属组
umask                 设置限制新文件权限的掩码
```

文件搜索
```
which                 查找环境变量中的文件
find                  查找目录和文件
locate                在mlocate数据库中搜索条目
updatedb              创建或更新slocate命令所必需的数据库文件
grep                  全面搜索正则表达式并把行打印出来
```

### 压缩解压命令

```
zip                   zip压缩工具
unzip                 解压缩zip文件
bzip2                 bzip2压缩工具
bunzip2               解压缩bzip2文件
gzip                  GNU zip
gunzip                GNU unzip
tar                   用来打包压缩和解压文件
```

### 帮助命令

```
man                   手册页
info                  以 Info 格式阅读文档
whatis                查询一个命令执行什么功能
apropos               在 whatis 数据库中查找字符串
```

### 重定向和常见符号

```
>                     输出重定向（覆盖）
>>                    输出重定向（追加）
<                     输入重定向

0<                    输入重定向
1>                    输出重定向
2>                    错误输出重定向
2>&1                  输出和错误输出重定向到一个地方
```
```
|                     管道符
/                     根目录
.                     当前目录
..                    上层目录
```

### 工具

```
date                  日期
cal                   日历
bc                    计算器
```

### 软件包管理

* [RPM](http://rpm.org/)
* [yum](http://yum.baseurl.org/)
* [apt](https://wiki.debian.org/Apt/)
* [Homebrew](http://brew.sh/)
* [MacPorts](https://www.macports.org/)

