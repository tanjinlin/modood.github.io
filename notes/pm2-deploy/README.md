# 使用 pm2 部署 Node 产品环境服务

## 基本步骤

*   实现无密码登录远程服务器

    *   使用ssh-keygen产生公钥私钥对

        ```bash
        ssh-keygen
        ```

    *   用ssh-copy-id将公钥复制到远程机器中

        ```bash
        # 安装
        brew install ssh-copy-id

        # ssh-copy-id 将key写到远程机器的 ~/ .ssh/authorized_key.文件中
        ssh-copy-id -i ~/.ssh/id_rsa.pub <username>@<host>
        ```

    *   参考资料

        *   [使用ssh-keygen和ssh-copy-id三步实现SSH无密码登录](http://blog.chinaunix.net/uid-26284395-id-2949145.html)
        *   [mac上使用ssh-copy-id 上传公钥 实现不输入密码登录](https://my.oschina.net/u/923974/blog/363757)
        *   [mac安装ssh-copy-id](http://www.01happy.com/mac-install-ssh-copy-id/)

*   实现无密码克隆或拉取代码

    *   [Generating an SSH key](https://help.github.com/articles/generating-an-ssh-key/)
    *   [Adding a new SSH key to your GitHub account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)

## 配置文件(ecosystem.json)

*   配置选项

    [PM2 Deployment](http://pm2.keymetrics.io/docs/usage/deployment/)

*   部署配置示例

    ```json
    {
      "deploy": {
        "prod": {
          "user": "mwn",
          "host": "120.24.254.22",
          "ref": "origin/master",
          "repo": "git@github.com:modood/koam.git",
          "path": "/home/mwn/workspace/koam",
          "post-deploy": "nvm use 7.1.0 && npm install && npm run doc && pm2 startOrRestart ecosystem.json --env prod",
          "env": {
            "NODE_ENV": "prod"
          }
        }
      }
    }
    ```

*   应用配置示例

    ```json
    {
      "apps": [
        {
          "name": "koam",
          "script": "app.js",
          "node_args": "--harmony",
          "env": {
            "COMMON_VARIABLE": "true"
          },
          "env_production": {
            "NODE_ENV": "prod"
          }
        }
      ]
    }
    ```

*   基本命令

    ```
    pm2 deploy ecosystem.json prod setup      首次部署初始化目录等
    pm2 deploy ecosystem.json prod            部署
    ```

*   注意问题

    * 每次部署会移除所有服务器本地修改的代码
    * 使用 `pm2 startOrRestart` 或使用 `pm2 start` 指定 `-i 1` 时 log4js 不生效（原因未知）

