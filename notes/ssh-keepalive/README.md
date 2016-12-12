# 如何保持 ssh 连接不断开

## 描述

用ssh链接服务端，一段时间不操作或屏幕没输出（比如复制文件）的时候，会自动断开

## 配置方法

*   在服务器端配置

    为了控制 ssh 的连接数，服务器希望断开一段时间无操作的连接，配置：

    ```bash
    vi  /etc/ssh/sshd_config
    ```
    ```
    TCPKeepAlive no
    ClientAliveInterval 60
    ClientAliveCountMax 3
    ```

*   在客户端配置

    客户端希望保持连接

    ```bash
    vi ~/.ssh/config
    ```
    ```
    Host *
       ServerAliveInterval 60
    ```

## 参考资料

*   [保持ssh连接不断](http://tonychiu.blog.51cto.com/656605/522304/)
*   [命令行终端保持连接](https://www.liaohuqiu.net/cn/posts/keep-alive-terminal-connection/)

