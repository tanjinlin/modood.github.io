# `child_process`

## `child_process`

*   创建子进程

    ```
    child_process.exec(command[, options][, callback])
    child_process.execSync(command[, options])
    child_process.execFile(file[, args][, options][, callback])
    child_process.execFileSync(file[, args][, options])

    child_process.spawn(command[, args][, options])
    child_process.spawnSync(command[, args][, options])

    child_process.fork(modulePath[, args][, options])
    ```

## child

*   事件

    ```
    close
    disconnect
    error
    exit
    message
    ```

*   流

    ```
    child.stdin
    child.stdout
    child.stderr
    child.stdio
    ```

*   子进程通信

    ```
    child.pid
    child.channel
    child.connected

    child.disconnect()
    child.kill([signal])
    child.send(message[, sendHandle[, options]][, callback])
    ```

