# 常用开发工具安装方法

目录

* 效率工具
    * [git](#git)
    * [git](#git)
    * [brew](#brew)
    * [wget](#wget)
    * [curl](#curl)
    * [oh](#oh)
    * [autojump](#autojump)
    * [tmux](#tmux)
    * [ack](#ack)
* 开发工具
    * [g++](#g++)
    * [nvm](#nvm)
    * [nginx](#nginx)
    * [mongodb](#mongodb)
    * [robomongo](#robomongo)
    * [redis](#redis)
    * [rabbitmq](#rabbitmq)

## 效率工具

### git

-   安装

    Ubuntu: `sudo apt-get install git`

    Centos: `sudo yum install git`

### git-extras

-   安装

    Mac: `sudo brew install git-extras`

### brew

-   安装

    Mac: `curl -LsSf http://github.com/mxcl/homebrew/tarball/master | sudo tar xvz -C/usr/local --strip 1`

### wget

-   安装

    Mac: `sudo brew install wget`

### curl

-   安装

    Ubuntu: `sudo apt-get install curl`

### oh-my-zsh

-   安装zsh

    Ubuntu: `sudo apt-get install zsh`

    Centos: `sudo yum install zsh`

    Mac: （默认自带）

-   安装oh-my-zsh

    方式一： curl

    `sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`

    方式二： wget

    `sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"`

-   设置为默认 shell (重启后生效)

    `chsh -s /bin/zsh`

-   配置文件

    `~/.zshrc`

-   使配置生效

    `source ~/.zshrc`

### autojump

-   安装:

    Ubuntu: `sudo apt-get install autojump`

    Centos: `sudo yum install autojump-zsh`

    Mac: `sudo brew install autojump`

-   配置: ~/.zshrc

    `plugins=(git autojump)`

-   使配置生效:

    `source ~/.zshrc`

### tmux

-   安装

    Ubuntu: `sudo apt-get install tmux`

    Centos: `sudo yum install -y tmux`

    Mac: `sudo brew install tmux`

-   配置

    默认前缀： `Ctrl + b`

    修改：

    ```
    tmux show-options -g        查看全局配置
    tmux set -g prefix C-s      修改前缀
    ```

-   保存快照

    [Tmux Resurrect](http://www.linuxidc.com/Linux/2015-07/120304.htm)

### ack

-   安装

    Ubuntu: `sudo apt-get install ack-grep`

    Centos: `sudo yum install ack`

    Mac: `sudo brew install ack`

## 开发工具

### g++

Centos

-   查看是否已安装

    ```
    $ rpm -qa | grep "g++"
    ```

-   查询可安装的相对应的功能的包

    ```
    $ yum whatprovides "*/g++"
    ```

    输出结果：

    ```
    gcc-c++-4.8.5-4.el7.x86_64 : C++ support for GCC
    Repo        : base
    Matched from:
    Filename    : /usr/bin/g++
    ```

-   安装 g++

    ```
    $ sudo yum install gcc-c++-4.8.5-4.el7.x86_64
    ```

### nvm & node

-   安装

    `wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.27.0/install.sh | bash`

    `nvm install 0.10.38`

    `nvm use 0.10.38`

    `npm install -g npm@2.9.0`

### nginx

Ubuntu

-   安装

    `sudo apt-get install nginx`

Centos

-   下载镜像包

    ```
    $ wget  http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
    ```

-   安装镜像源

    ```
    $ sudo rpm -ivh nginx-release-centos-7-0.el7.ngx.noarch.rpm
    ```

-   安装

    ```
    $ sudo yum install nginx
    ```

-   启动

    ```
    $ sudo systemctl start nginx
    ```

Mac

-   安装

    ```
    $ sudo brew install nginx
    ```

-   启动

    ```
    $ sudo nginx [-c config_file]
    ```

-   配置文件

    ```
    /usr/local/etc/nginx/nginx.conf
    ```

### mongodb

Ubuntu

-   安装

    Ubuntu: `sudo apt-get install mongodb`

Centos

-   简介

    包含的组件：

    ```
    mongodb-org         A metapackage that will automatically install the four component packages listed below.
    mongodb-org-server  Contains the mongod daemon and associated configuration and init scripts.
    mongodb-org-mongos  Contains the mongos daemon.
    mongodb-org-shell   Contains the mongo shell.
    mongodb-org-tools   Contains the following MongoDB tools: mongoimport bsondump, mongodump, mongoexport, mongofiles, mongooplog, mongoperf, mongorestore, mongostat, and mongotop.
    ```

-   下载

    ```
    $ wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-amazon-3.2.7.tgz
    ```

-   安装

    ```
    $ tar -zxvf mongodb-linux-x86_64-amazon-3.2.7.tgz
    $ sudo mv mongodb-linux-x86_64-amazon-3.2.7 /usr/local/lib

    $ sudo ln -s /usr/local/lib/mongodb-linux-x86_64-amazon-3.2.7/bin/mongod /usr/bin/mongod

    $ sudo ln -s /usr/local/lib/mongodb-linux-x86_64-amazon-3.2.7/bin/mongo /usr/local/bin/mongo
    $ sudo ln -s /usr/local/lib/mongodb-linux-x86_64-amazon-3.2.7/bin/mongoexport /usr/local/bin/mongoexport
    ```

-   创建数据和日志文件目录

    ```
    $ sudo mkdir -p /var/lib/mongodb
    $ sudo mkdir -p /var/log/mongodb
    $ sudo touch /var/log/mongodb/mongod.log
    ```

-   创建配置文件

    ```
    $ sudo vi /etc/mongod.conf
    ```
    ```
    # mongod.conf

    # for documentation of all options, see:
    #   http://docs.mongodb.org/manual/reference/configuration-options/

    # Where and how to store data.
    storage:
      dbPath: /var/lib/mongodb
      journal:
        enabled: true

    # where to write logging data.
    systemLog:
      destination: file
      logAppend: true
      path: /var/log/mongodb/mongod.log

    # network interfaces
    net:
      port: 27017
      bindIp: 127.0.0.1
    ```

-   启动

    ```
    $ sudo mongod -f /etc/mongod.conf &
    ```

Mac

-   安装

    ```
    $ sudo brew install mongodb
    ```

-   启动

    使用默认配置文件，启动在后台：

    ```
    $ brew services start mongodb
    ```

    指定配置文件：

    ```
    $ mongod --config /usr/local/etc/mongod.conf
    ```

-   配置文件

    ```
    /usr/local/etc/mongod.conf
    ```
    ```
    systemLog:
      destination: file
      path: /usr/local/var/log/mongodb/mongo.log
      logAppend: true
    storage:
      dbPath: /usr/local/var/mongodb
    net:
      bindIp: 127.0.0.1
    ```

### robomongo

Centos

-   下载

    ```
    wget https://download.robomongo.org/0.9.0-rc8/linux/robomongo-0.9.0-rc8-linux-x86_64-c113244.tar.gz
    ```

-   安装

    ```
    $ tar -zxvf robomongo-0.9.0-rc8-linux-x86_64-c113244.tar.gz
    $ sudo mv robomongo-0.9.0-rc8-linux-x86_64-c113244 /usr/local/lib
    $ sudo ln -s /usr/local/lib/robomongo-0.9.0-rc8-linux-x86_64-c113244/bin/robomongo /usr/local/bin/robomongo
    ```

### redis

Ubuntu

-   安装

    `sudo apt-get install redis-server`

Centos

-   下载

    ```
    $ wget http://download.redis.io/releases/redis-3.0.3.tar.gz
    ```

-   安装

    ```
    $ tar zxvf redis-3.0.3.tar.gz
    $ sudo mv redis-3.0.3 /usr/local/lib/
    $ cd /usr/local/lib/redis-3.0.3/
    $ make
    $ sudo ln -s /usr/local/lib/redis-3.0.3/src/redis-server /usr/bin/redis-server
    $ sudo ln -s /usr/local/lib/redis-3.0.3/src/redis-cli /usr/local/bin/redis-cli
    ```

-   创建数据和日志文件目录

    ```
    $ sudo mkdir -p /var/lib/redis
    $ sudo mkdir -p /var/log/redis
    $ sudo touch /var/log/redis/redis-server.log
    ```

-   编辑配置文件

    ```
    $ sudo vi /usr/local/lib/redis-3.0.3/redis.conf
    ```
    ```
    logfile /var/log/redis/redis-server.log

    dir /var/lib/redis
    dbfilename dump.rdb
    ```

-   设置密码

    ```
    $ sudo vi /usr/local/lib/redis-3.0.3/redis.conf
    ```
    ```
    requirepass yourpassword
    ```

    密码验证:

    ```
    $ redis-cli -a yourpassword
    ```

-   启动

    ```
    $ sudo redis-server /usr/local/lib/redis-3.0.3/redis.conf &
    ```

Mac

-   下载

    ```
    $ wget http://download.redis.io/releases/redis-3.2.0.tar.gz
    ```

-   安装

    解压移动到：

    ```
    /usr/local/software/
    ```

    安装：

    ```
    $ make
    $ sudo make install
    ```

    复制配置文件：

    ```
    $ sudo cp redis.conf /usr/local/etc/
    ```

-   配置文件

    ```
    /usr/local/etc/redis.conf
    ```
    ```
    dbfilename dump.rdb
    dir /usr/local/var/redis

    logfile /usr/local/var/log/redis/redis.log
    ```

-   启动

    ```
    $ sudo redis-server /usr/local/etc/redis.conf &
    ```

### rabbitmq

Ubuntu

-   安装

    ```
    wget https://www.rabbitmq.com/rabbitmq-signing-key-public.asc
    sudo apt-key add rabbitmq-signing-key-public.asc

    apt-get update.
    sudo apt-get install rabbitmq-server

    sudo rabbitmqctl stop
    sudo rabbitmq-plugins enable rabbitmq_management
    sudo rabbitmq-server

    http://127.0.0.1:15672/
    默认用户：guest，密码：guest
    ```

Mac

-   安装

    ```
    $ sudo brew install rabbitmq
    ```

-   创建软连接

    ```
    $ sudo ln -s /usr/local/Cellar/rabbitmq/3.6.1/sbin/rabbitmq-defaults /usr/local/bin/rabbitmq-defaults
    $ sudo ln -s /usr/local/Cellar/rabbitmq/3.6.1/sbin/rabbitmq-env /usr/local/bin/rabbitmq-env
    $ sudo ln -s /usr/local/Cellar/rabbitmq/3.6.1/sbin/rabbitmq-plugins /usr/local/bin/rabbitmq-plugins
    $ sudo ln -s /usr/local/Cellar/rabbitmq/3.6.1/sbin/rabbitmq-server /usr/local/bin/rabbitmq-server
    $ sudo ln -s /usr/local/Cellar/rabbitmq/3.6.1/sbin/rabbitmqadmin /usr/local/bin/rabbitmqadmin
    $ sudo ln -s /usr/local/Cellar/rabbitmq/3.6.1/sbin/rabbitmqctl /usr/local/bin/rabbitmqctl
    ```

-   启动

    ```
    $ brew services start rabbitmq
    ```

    或：

    ```
    $ rabbitmq-server
    ```

-   后台管理

    默认用户名密码 guest

    ```
    http://127.0.0.1:15672
    ```
