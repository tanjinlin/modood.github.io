# process

the current Node.js process

without using require()

The process object is an instance of EventEmitter

## Events

*   Process Events:

    ```
    beforeExit
    exit
    warning
    message
    disconnect
    unhandledRejection
    rejectionHandled
    uncaughtException
    ```

*   [Signal Events](http://man7.org/linux/man-pages/man7/signal.7.html)

    ```
    SIGINT
    SIGHUP
    ...
    ```

## Properties and Methods

*   流

    ```
    process.stdin
    process.stdout
    process.stderr
    ```

*   进程信息

    ```
    process.arch
    process.platform
    process.version
    process.versions
    process.release
    process.config
    process.env
    process.argv
    process.argv0
    process.execArgv
    process.execPath
    process.pid
    process.title
    process.cwd()
    process.chdir(directory)
    process.uptime()
    process.mainModule
    ```

*   进程管理

    ```
    process.exitCode
    process.exit([code])
    process.abort()
    process.kill(pid[, signal])
    ```

*   事件相关

    ```
    process.nextTick(callback)
    process.emitWarning(warning[, name][, ctor])
    ```

*   子进程

    ```
    process.execArgv
    process.umask([mask])
    ```

*   进程间通信

    ```
    process.channel
    process.connected
    process.disconnect()
    process.send(message[, sendHandle[, options]][, callback])
    ```

*   用户和组

    ```
    process.getuid()
    process.setuid(id)
    process.getgid()
    process.setgid(id)
    process.geteuid()
    process.seteuid(id)
    process.getegid()
    process.setegid(id)
    process.getgroups()
    process.setgroups(groups)
    process.initgroups(user, extra_group)
    ```

*   性能检查

    ```
    process.hrtime([time])
    process.cpuUsage([previousValue])
    process.memoryUsage()
    ```
