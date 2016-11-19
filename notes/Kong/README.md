# API Gateway: Kong 基本部署和使用

##  安装（Installation）

-   在 Ubuntu 下安装

    ```
    wget https://github.com/Mashape/kong/releases/download/0.8.2/kong-0.8.2.vivid_all.deb

    sudo apt-get update
    sudo apt-get install netcat openssl libpcre3 dnsmasq procps
    sudo dpkg -i kong-0.8.2.*.deb
    ```

-   在 Centos 下安装

    ```
    wget https://github.com/Mashape/kong/releases/download/0.8.3/kong-0.8.3.el7.noarch.rpm

    sudo yum install epel-release
    sudo yum install kong-0.8.3.*.noarch.rpm --nogpgcheck
    ```

##  配置（Configuration Reference）

-   默认配置文件

    ```
    Using configuration: /etc/kong/kong.yml
    ```

-   配置 postgres 数据库

    ```
    ######
    ## Specify which database to use. Only "cassandra" and "postgres" are currently available.
    database: postgres

    ######
    ## PostgreSQL configuration
    postgres:
      host: "127.0.0.1"
      port: 5432

      ######
      ## Name of the database used by Kong. Will be created if it does not exist.
      database: postgres

      #####
      ## User authentication settings
      user: "postgres"
      password: "postgres"
    ```

-   注意事项

    1.  postgreSQL 9.4 以上

    2.  如果报错：　[ERR] FATAL: Ident authentication failed for user "postgres"

        修改　pg_hba.conf　文件将　peer 或 ident 改为 md5

##  命令行工具（CLI Reference）

-   基本命令

    ```
    $ kong start                        启动
    $ kong stop                         停止
    $ kong quit                         退出
    $ kong reload                       重启
    $ kong reload                       重载
    $ kong status                       查看状态
    $ kong migrations                   数据迁移
    $ kong cluster                      集群
    ```

## 集群（Clustering Reference）

-   参考资料

    <https://getkong.org/docs/0.8.x/clustering/>

## 代理（Proxy Reference）

-   Proxy an API by its DNS values

    ```
    Using the "Host" header
    Using the "X-Host-Override" header
    Using the "request_host" header
    ```

-   Proxy an API by its request_path value

    ```
    Using the "strip_request_path" property
    ```

## 网络和防火墙（Network & Firewall）

-   端口号

    Kong listens on several ports that must allow external traffic and are by default:

    ```
    8000 for proxying. This is where Kong listens for HTTP traffic. Be sure to change it to 80 once you go to production. See proxy_listen.
    8443 for proxying HTTPS traffic. Be sure to change it to 443 once you go to production. See [proxy_ssl_listen].
    7946 which Kong uses for inter-nodes communication. Both UDP and TCP traffic should be allowed on it. See cluster_listen.
    ```

    Additionally, those ports are used internally and should be firewalled in production usage:

    ```
    8001 provides Kong's Admin API that you can use to operate Kong. See admin_api_listen.
    7373 used by Kong to communicate with the local clustering agent. See cluster_listen_rpc.
    ```

## 管理（admin api）

-   添加 API 服务

    ```
    POST http://localhost:8001/apis/
    ```

    请求参数：

    ```
    {
        "name":"notification",
        "request_host":"notification.example.com",
        "request_path":"/notification",
        "strip_request_path":"true",
        "upstream_url":"http://notification.example.com/"
    }
    ```

    返回结果：

    ```
    {
        "upstream_url": "http://notification.example.com/",
        "created_at": 1464921526000,
        "request_path": "/notification",
        "id": "cdbf6854-88bd-427c-a383-fd90541e6d7e",
        "name": "notification",
        "preserve_host": false,
        "strip_request_path": true,
        "request_host": "notification.example.com"
    }
    ```

-  添加插件

    ```
    POST http://127.0.0.1:8001/apis/notification/plugins
    ```

    请求参数：

    ```
    {
        "name": "jwt"
    }
    ```

    返回结果:

    ```
    {
      "api_id": "cdbf6854-88bd-427c-a383-fd90541e6d7e",
      "id": "780e33d3-42f7-416a-8ab0-4306976c1026",
      "created_at": 1465121014000,
      "enabled": true,
      "name": "jwt",
      "config": {
        "uri_param_names": [
          "jwt"
        ],
        "secret_is_base64": false,
        "key_claim_name": "iss"
      }
    }
    ```

-   创建 Consumer

    ```
    POST http://127.0.0.1:8001/consumers
    ```

    请求参数：

    ```
    {
        "username": "mwn",
        "custom_id": "55c1c7e6d56603030a7a9e84"
    }
    ```

    返回结果：

    ```
    {
      "custom_id": "55c1c7e6d56603030a7a9e84",
      "username": "mwn",
      "created_at": 1465121260000,
      "id": "98966f9e-39fc-4e0f-bced-57cc46f9ebdd"
    }
    ```

-   创建 JWT 凭证

    ```
    curl -X POST http://127.0.0.1:8001/consumers/mwn/jwt
    POST http://127.0.0.1:8001/consumers/mwn/jwt
    ```

    请求参数：

    ```
    {}
    ```

    返回结果：

    ```
    {
      "secret": "39b9827b04fe44fe8686d8793758719b",
      "id": "8c5b663b-f248-4cf8-9451-9aa07466b62c",
      "algorithm": "HS256",
      "created_at": 1465122023000,
      "key": "081dcbfcfe1144169d6e423ab603ae76",
      "consumer_id": "98966f9e-39fc-4e0f-bced-57cc46f9ebdd"
    }
    ```

-   生成 JWT

    生成方法：

    ```
    var jwt = require('jsonwebtoken');

    var token = jwt.sign({
        "typ": "JWT",
        "alg": "HS256",
        "iss": "081dcbfcfe1144169d6e423ab603ae76"
    }, '39b9827b04fe44fe8686d8793758719b');

    console.log(token)
    ```

    返回结果：

    ```
    eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiIsImlzcyI6IjA4MWRjYmZjZmUxMTQ0MTY5ZDZlNDIzYWI2MDNhZTc2IiwiaWF0IjoxNDY1MTIyMTMzfQ.FpQ8arFSDIrXI1Mn_VZnO1qSAqw5c3P0TC55PToqacc
    ```

-   模拟访问

    使用 uri_param_names 参数：

    ```
    curl http://127.0.0.1:8000/notification?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiIsImlzcyI6IjA4MWRjYmZjZmUxMTQ0MTY5ZDZlNDIzYWI2MDNhZTc2IiwiaWF0IjoxNDY1MTIyMTMzfQ.FpQ8arFSDIrXI1Mn_VZnO1qSAqw5c3P0TC55PToqacc
    ```

    使用  Authorization header:

    ```
    curl http://127.0.0.1:8000/notification -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiIsImlzcyI6IjA4MWRjYmZjZmUxMTQ0MTY5ZDZlNDIzYWI2MDNhZTc2IiwiaWF0IjoxNDY1MTIyMTMzfQ.FpQ8arFSDIrXI1Mn_VZnO1qSAqw5c3P0TC55PToqacc'
    ```

-   解析正确

    服务器端获取到 http req headers

    ```
    headers:
    {
        'x-consumer-id': '98966f9e-39fc-4e0f-bced-57cc46f9ebdd',
        'x-consumer-custom-id': '55c1c7e6d56603030a7a9e84',
        'x-consumer-username': 'mwn'
    },
    ```
