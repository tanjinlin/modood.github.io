# Centos 下开发常见遇到的问题以及解决方案

## CentOS下如何挂载NTFS分区

-   下载 rpmforge

    32 位：

    ```
    $ wget http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.2-1.el6.rf.i686.rpm
    ```

    64 位：

    ```
    $ wget http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm
    ```

-   安装 rpmforge

    ```
    $ rpm -ivh rpmforge-release-0.5.2-1.el6.rf.i686.rpm
    ```

-   安装 wntfs-3g

    ```
    $ sudo yum install ntfs-3g
    ```

-   参考资料

    http://www.eechina.com/blog-53984-3714.html

    http://blog.chinaunix.net/uid-20752341-id-3289253.html

## 修复 /lib/ld-linux.so.2 报错问题

-   报错描述

    ```
    /lib/ld-linux.so.2: bad ELF interpreter: No such file or directory
    ```

-   问题原因

    在64系统里执行32位程序

-   解决办法

    ```
    $ sudo yum install glibc.i686
    ```

-   参考资料

    http://www.2cto.com/os/201207/142437.html

## Centos 下 g++ 安装

-   问题描述

    如果直接键入: `sudo yum install g++` 会提示 `没有可用软件包 g++`

-   解决办法

    使用 `sudo yum install gcc-c++`，这才是这个包的名字。

-   参考资料

    http://blog.sina.com.cn/s/blog_6f561cc301015emv.html

