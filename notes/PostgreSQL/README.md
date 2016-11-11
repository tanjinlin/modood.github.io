# PostgreSQL 学习笔记

## 基础

-   安装

    Ubuntu:

    ```
    sudo apt-get install postgresql-9.4
    ```

    Centos:
    ```
    sudo yum install postgresql-server

    sudo service postgresql initdb
    sudo chkconfig postgresql on
    ```

-   默认信息

    ```
    config /etc/postgresql/9.4/main
    data   /var/lib/postgresql/9.4/main
    port   5432
    ```

-   修改 linux 系统 postgres 用户的密码：

    ```
    sudo passwd -d postgres             清空密码
    sudo -u postgres passwd             修改密码
    su postgres                         切换用户
    ```

-   修改 postgreSQL 数据库 postgres 用户的密码：

    ```
    sudo -u postgres psql
    ALTER USER postgres WITH PASSWORD 'postgres';
    ```

-   常用命令

    ```
    createuser kong -P              创建用户
    dropuser kong                   删除用户
    createdb kong                   创建数据库
    dropdb kong                     删除数据库
    ```

    ```
    \q                              退出 psql
    \password postgres              设置密码
    \h                              查看SQL命令的解释，比如\h select。
    \?                              查看psql命令列表。
    \l                              列出所有数据库。
    \c [database_name]              连接其他数据库。
    \d                              列出当前数据库的所有表格。
    \d [table_name]                 列出某一张表格的结构。
    \du                             列出所有用户。
    \e                              打开文本编辑器。
    \conninfo                       列出当前数据库和连接的信息。
    ```

-   启动

    ```
    postgres -D ~/data/ > ~/logs/pg_server.log 2>&1 &
    ```

-   登录

    ```
    sudo -u postgres psql
    psql -U postgres -d postgres -h 127.0.0.1 -p 5432
    psql -U postgres -d postgres -h 127.0.0.1 -p 5432 -c "select * from apis" postgres
    ```

## 参考资料

* [PostgreSQL新手入门](http://www.ruanyifeng.com/blog/2013/12/getting_started_with_postgresql.html)
* [PostgreSQL 角色与用户管理介绍](http://www.jb51.net/article/40300.htm)
* [修改postgres的密码](http://www.360doc.com/content/13/0822/10/10384031_309039914.shtml)
* [PostgreSQL服务器启动和关闭方法介绍](http://blog.csdn.net/dyx1024/article/details/6594851)
