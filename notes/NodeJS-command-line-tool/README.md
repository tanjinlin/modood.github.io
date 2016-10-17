# 使用 NodeJS 开发命令行工具

## 创建 package.json

-   `npm init`

    生成 package.json 文件后需要设置一下 bin 字段。

    bin 类型为 object ，属性名称为最终生成的命令行工具命令名称（示例为 hit ），属性值为执行命令时将会执行的脚本文件（示例为 bin/hit.js 文件）。

    ```json
    {
      "name": "node-command-line-tool",
      "version": "1.0.0",
      "description": "To make a node command line tool",
      "main": "index.js",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "preferGlobal": "true",
      "bin": {
        "hit": "bin/hit.js"
      },
      "keywords": [
        "command",
        "line"
      ],
      "author": "modood",
      "license": "ISC"
    }
    ```

## 编写脚本代码

-   安装 commander

    ```
    $ npm install commander --save
    ```

    [Commander.js](https://github.com/tj/commander.js) 是 [TJ](https://github.com/tj/) 写的一个帮助快速开发Nodejs命令行工具的模块。它的方便之处在于：

    ```
    1. 解析命令行参数
    2. 方便的定义option(包括option的描述和其回调函数)和子命令
    ```

-   创建 bin/hit.js 文件：

    ```javascript
    #!/usr/bin/env node

    var program = require('commander');

    program
      .version('0.0.1')
      .option('-p, --print', 'print Hello World')
      .parse(process.argv);

    if (program.print) {
      console.log('Hello World');
    };

    console.log('wow! you made it!');
    ```

## 完成

-   本地创建链接文件测试效果：

    ```
    $ sudo npm link
    ```

    重新打开终端，可以执行：

    ```
    $ hit -h

      Usage: hit [options]

      Options:

        -h, --help     output usage information
        -V, --version  output the version number
        -p, --print    print Hello World
    ```

-   发布到 NPM 上

    登录：

    ```
    $ npm login
    ```

    发布：

    ```
    $ npm publish
    ```
