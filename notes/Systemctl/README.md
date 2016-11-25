# 使用 Systemctl 管理服务器服务

## 简介

Systemctl: 一个systemd工具，主要负责控制systemd系统和服务管理器。

Systemd: 一个系统管理守护进程、工具和库的集合，用于集中管理和配置类UNIX系统。

## 基本命令

*   查看版本

    ```bash
    systemctl --version
    ```

*   检查systemd是否运行

    ```bash
    ps -eaf | grep [s]ystemd
    ```

*   分析systemd启动进程

    ```bash
    systemd-analyze

    # 各个进程花费的时间
    systemd-analyze blame

    # 关键链
    systemd-analyze critical-chain
    ```

*   按等级列出控制组

    ```bash
    systemd-cgls
    ```

*   按CPU、内存、输入和输出列出控制组

    ```bash
    systemd-cgtop
    ```

## 单元

*   接受的单元

    *   服务（.service）
    *   挂载点（.mount）
    *   套接口（.socket）
    *   设备（.device）

*   列出所有可用单元

    ```bash
    systemctl list-unit-files

    # 列出所有服务
    systemctl list-unit-files --type=service
    ```

*   列出所有运行中单元

    ```bash
    systemctl list-units
    ```

*   列出所有失败单元

    ```bash
    systemctl --failed
    ```

*   启动、重启、停止、重载

    ```bash
    systemctl start httpd.service
    systemctl restart httpd.service
    systemctl stop httpd.service
    systemctl reload httpd.service
    systemctl status httpd.service
    ```

*   杀死服务

    ```bash
    systemctl kill httpd
    ```

*   检查某个单元是否启用

    ```bash
    systemctl is-enabled crond.service
    systemctl is-active crond.service
    ```

*   开机自启

    ```bash
    systemctl enable httpd.service
    systemctl disable httpd.service
    ```

*   屏蔽或显示

    ```bash
    systemctl mask httpd.service
    systemctl unmask httpd.service
    ```

*   依赖性列表

    ```bash
    systemctl list-dependencies
    ```

*   查看、设置属性

    ```bash
    systemctl show httpd.service

    # 获取某个服务的CPU分配额
    systemctl show -p CPUShares httpd.service

    # 限制某个服务的CPU分配额
    systemctl set-property httpd.service CPUShares=2000
    ```

## 系统管理

*   运行等级

    ```
    Runlevel0：系统关闭，系统默认运行级别不能设为0，否则不能正常启动
    Runlevel1：单用户工作状态，root权限，用于系统维护，禁止远程登陆
    Runlevel2：多用户状态(没有NFS)
    Runlevel3：完全的多用户状态(有NFS)，登陆后进入控制台命令行模式
    Runlevel4：系统未使用，保留
    Runlevel5：X11控制台，登陆后进入图形GUI模式
    Runlevel6：系统正常关闭并重启，默认运行级别不能设为6，否则不能正常启动
    ```

*   默认运行等级

    ```bash
    # 查看
    systemctl get-default

    # 设置默认运行等级
    systemctl set-default runlevel3.target
    ```

*   救援模式

    ```bash
    systemctl rescue
    ```

*   紧急模式

    ```bash
    systemctl emergency
    ```

*   等级5，即图形模式

    ```bash
    systemctl isolate runlevel5.target
    # or
    systemctl isolate graphical.target
    ```

*   等级3，即多用户模式

    ```bash
    systemctl isolate runlevel3.target
    # or
    systemctl isolate multiuser.target
    ```

*   重启、停止、挂起、休眠系统或使系统进入混合睡眠

    ```bash
    systemctl reboot
    systemctl halt
    systemctl suspend
    systemctl hibernate
    systemctl hybrid-sleep
    ```

## 示例：使用systemctl 管理 mongodb 服务

*   编辑 mongod.service 文件

    ```bash
    vi /usr/lib/systemd/system/mongod.service
    ```
    ```
    [Unit]
    Description=mongodb database

    [Service]
    Environment="OPTIONS=--quiet -f /etc/mongod.conf"
    ExecStart=/usr/bin/mongod $OPTIONS

    [Install]
    WantedBy=multi-user.target
    ```

*   创建链接文件

    ```bash
    ln -s /usr/lib/systemd/system/mongod.service /etc/systemd/system/multi-user.target.wants/
    ```

*   重新加载systemctl

    ```bash
    systemctl daemon-reload
    ```

*   启动

    ```bash
    systemctl start mongod
    ```

*   停止

    ```bash
    systemctl stop mongod
    ```

## 参考资料

*   [systemctl 命令完全指南](https://linux.cn/article-5926-1.html)

