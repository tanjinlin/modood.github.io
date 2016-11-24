# readline

## Class: Interface

*   事件

    ```
    line
    pause
    resume
    close
    SIGCONT
    SIGINT
    SIGTSTP
    ```

*   创建

    ```
    readline.createInterface(options)
    ```

*   操作

    ```
    rl.setPrompt(prompt)

    rl.prompt([preserveCursor])
    rl.write(data[, key])

    rl.question(query, callback)

    rl.close()
    rl.pause()
    rl.resume()
    ```

*   操作鼠标

    ```
    readline.cursorTo(stream, x, y)
    readline.moveCursor(stream, dx, dy)
    ```

*   清屏

    ```
    readline.clearLine(stream, dir)
    readline.clearScreenDown(stream)
    ```

*   其它

    ```
    readline.emitKeypressEvents(stream[, interface])
    ```

