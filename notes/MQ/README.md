# 消息队列

## 基础

*   简介

    MQ全称为Message Queue, 消息队列（MQ）是一种应用程序对应用程序的通信方法。

    MQ是消费-生产者模型的一个典型的代表，一端往消息队列中不断写入消息，而另一端则可以读取或者订阅队列中的消息。

    在项目中，将一些无需即时返回且耗时的操作提取出来，进行了异步处理，而这种异步处理的方式大大的节省了服务器的请求响应时间，从而提高了系统的吞吐量。

*   RabbitMQ

    本身支持很多的协议：AMQP，XMPP, SMTP, STOMP，也正是如此，使的它变的非常重量级，更适合于企业级的开发。
    同时实现了一个经纪人(Broker)构架，这意味着消息在发送给客户端时先在中心队列排队。
    对路由(Routing)，负载均衡(Load balance)或者数据持久化都有很好的支持。

*   ZeroMQ

    号称最快的消息队列系统，尤其针对大吞吐量的需求场景。

    ZeroMQ具有一个独特的非中间件的模式，你不需要安装和运行一个消息服务器或中间件，因为你的应用程序将扮演了这个服务角色。
    你只需要简单的引用ZeroMQ程序库，可以使用NuGet安装，然后你就可以愉快的在应用程序之间发送消息了。

    但是ZeroMQ仅提供非持久性的队列，也就是说如果down机，数据将会丢失。

*   Jafka/Kafka

    Kafka是Apache下的一个子项目，是一个高性能跨语言分布式Publish/Subscribe消息队列系统，而
    Jafka是在Kafka之上孵化而来的，即Kafka的一个升级版。

    具有以下特性：快速持久化，高吞吐，完全的分布式系统，支持Hadoop数据并行加载。

# RabbitMQ 学习

## 安装(CentOS Linux release 7.2.1511)

*   Install Erlang

    ```bash
    # Install Erlang from the EPEL repository
    yum install erlang
    ```

*   Install RabbitMQ Server

    ```bash
    # Download the server package, from rabbitmq.com
    wget https://github.com/rabbitmq/rabbitmq-server/releases/download/rabbitmq_v3_6_6/rabbitmq-server-3.6.6-1.el7.noarch.rpm
    # Download the server package, from github.com
    wget http://www.rabbitmq.com/releases/rabbitmq-server/v3.6.6/rabbitmq-server-3.6.6-1.el7.noarch.rpm

    # Issue the following command as 'root'
    rpm --import https://www.rabbitmq.com/rabbitmq-release-signing-key.asc
    yum install rabbitmq-server-3.6.6-1.el7.noarch.rpm
    ```

*   Start/Stop the Server

    ```bash
    # start
    systemctl start rabbitmq-server

    # stop
    systemctl stop rabbitmq-server
    ```

*   Enable Management Plugin

    ```bash
    # Enable
    rabbitmq-plugins enable rabbitmq_management

    # The web UI is located at: http://server-name:15672/
    # On a fresh installation the user "guest" is created with password "guest"
    # By default, the guest user is prohibited from connecting to the broker remotely

    # Add user
    rabbitmqctl add_user mwn 10086
    # Set administrator
    rabbitmqctl set_user_tags mwn administrator
    ```

## 管理和监控

*   management plugin

    基于 Web 界面管理：http://www.rabbitmq.com/management.html

    基于命令行工具 rabbitmqadmin 管理：http://www.rabbitmq.com/management-cli.html

*   rabbitmqctl

    命令文档：http://www.rabbitmq.com/man/rabbitmqctl.1.man.html

## 基本概念

*   生产者（producer）

*   队列（queue） 

*   消费者（consumer）

## 项目开发

*   [RabbitMQ Tutorials](http://www.rabbitmq.com/getstarted.html)
*   [amqp.node](https://github.com/squaremo/amqp.node)

## 参考资料

*   [【消息队列MQ】各类MQ比较](http://blog.csdn.net/sunxinhere/article/details/7968886)

