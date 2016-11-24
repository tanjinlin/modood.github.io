# vm

*   Context

    ```
    vm.createContext([sandbox])

    vm.isContext(sandbox)

    vm.runInContext(code, contextifiedSandbox[, options])
    vm.runInNewContext(code[, sandbox][, options])
    vm.runInThisContext(code[, options])
    vm.runInDebugContext(code)
    ```

*   Script

    ```
    new vm.Script(code, options)

    script.runInContext(contextifiedSandbox[, options])
    script.runInNewContext([sandbox][, options])
    script.runInThisContext([options])
    ```

