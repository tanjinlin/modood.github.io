# console

*   Class: Console

    ```
    new console.Console(stdout[, stderr])
    ```

    实际上，全局的 console 是一个特殊的 Console 实例，只不过它的输出和错误输出流指向了 process.stdout 和 process.stderr

*   console

    ```
    console.log([data][, ...args])
    console.info([data][, ...args])
    console.dir(obj[, options])

    console.warn([data][, ...args])
    console.error([data][, ...args])
    console.trace(message[, ...args])

    console.assert(value[, message][, ...args])

    console.time(label)
    console.timeEnd(label)
    ```
