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

### 文件处理命令

```
ls          list                            /bin/ls         -a 显示所有文件，包括隐藏文件
                                                            -l 显示详细信息
                                                            -d 查看目录属性
cd          change directory                Shell 内置
pwd         print working directory         /bin/pwd
touch                                       /bin/touch
mkdir       make directory                  /bin/mkdir
cp          copy                            /bin/cp         -R 复制目录
mv          move                            /bin/mv
rm          remove                          /bin/rm         -r 删除目录
cat         concatenate and display files   /bin/cat
more                                        /bin/more
head                                        /bin/head       -n 显示文件前 n 行
tail                                        /bin/tail       -n 显示文件后 n 行
                                                            -f 动态显示文件内容
ln                                          /bin/ln         -s 创建软链接
```

### 权限管理命令

```
chmod       change the permissions modes    /bin/chmod
chown       change file ownership           /bin/chown
chgrp       change file group ownership     /bin/chgrp
umask                                       /bin/umask
```

### 文件搜索命令

```
which                                       /usr/bin/which
find                                        /usr/bin/find
locate                                      /usr/bin/locate
updatedb    update the slocate database     /usr/bin/updatedb
grep                                        /bin/grep
```

### 帮助命令

```
man         manual                          /usr/bin/man
info        information                     /usr/bin/info
whatis                                      /usr/bin/whatis
apropos                                     /usr/bin/apropos
makewhatis                                  /usr/sbin/makewhatis
```

### 压缩解压命令

```
zip                                         /usr/bin/zip        -r 压缩目录
unzip                                       /usr/bin/unzip
bzip2                                       /usr/bin/bzip2      -k 产生压缩文件后保留原文件
bunzip2                                     /usr/bin/bunzip2    -k 解压缩后保留原文件
gzip        GNU zip                         /bin/gzip
gunzip      GNU unzip                       /bin/unzip
tar                                         /bin/tar            -c 产生 .tar 打包文件
                                                                -v 显示详细信息
                                                                -f 指定压缩后的文件名
                                                                -z 打包同时压缩
                                                                -x 解包
```

### 网络通信命令

```
write                                       /usr/bin/write
wall                                        /usr/bin/wall
ping                                        /usr/sbin/ping
ifconfig                                    /usr/sbin/ifconfig  -a 显示所有网卡信息
```

### 系统关机命令

```
shutdown                                    /usr/sbin/shutdown
reboot                                      /usr/sbin/reboot
```
