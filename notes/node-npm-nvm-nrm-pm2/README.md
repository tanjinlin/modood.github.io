# 常用的 node, npm, nvm, nrm, pm2 命令

## [node](https://github.com/nodejs/node)

-   常用命令

    ```
    node --v8-options                     查看 v8 选项
    node --v8-options | grep harmony      查看 ES6 特性
    node --inspect                        使用 Chrome DevTools 调试
    ```

## [npm](https://github.com/npm/npm)

-   简介

    Node Package Manager

-   常用命令

    ```
    npm init                              初始化 package.json 文件
    npm search                            查找
    npm view                              查看
    npm docs                              查看文档
    npm install                           安装
    npm uninstall                         卸载
    npm outdated                          查看过时的依赖
    npm update                            更新
    npm shrinkwrap                        锁定依赖的版本
    npm login                             登录
    npm link                              链接包
    npm unlink                            取消链接包
    npm publish                           发布包
    npm unpublish                         取消发布包
    ``

## [nvm](https://github.com/creationix/nvm)

-   简介

    Node Version Manager

-   常用命令

    ```
    nvm ls                                列出已安装的版本列表
    nvm ls-remote                         列出所有版本
    nvm install                           安装
    nvm uninstall                         卸载
    nvm current                           查看当前使用的版本
    nvm use                               切换版本
    nvm alias default 0.10.38             设置默认版本
    ```

## [nrm](https://github.com/Pana/nrm)

-   简介

    NPM Registry Manager

-   常用命令

    ```
    nrm ls                                列出可以使用的源
    nrm use                               切换源
    ```

## [pm2](https://github.com/Unitech/pm2)

-   简介

    Production process manager

-   常用命令

    ```
    pm2 start                             启动进程
    pm2 describe                          进程信息
    pm2 list                              进程列表
    pm2 stop                              停止进程
    pm2 restart                           重启进程
    pm2 delete                            停止并删除进程
    pm2 logs                              查看日志
    pm2 flush                             清除日志
    pm2 monit                             监控
    pm2 web                               管理API(端口：9615 )
    pm2 save                              保存快照
    pm2 resurrect                         恢复
    pm2 deploy                            部署
    ```

