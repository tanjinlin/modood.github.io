# events

## Class: EventEmitter

*   事件

    ```
    error
    newListener
    removeListener
    ```

*   最多监听器数量

    ```
    EventEmitter.defaultMaxListeners

    emitter.getMaxListeners()
    emitter.setMaxListeners(n)
    ```

*   事件分发器信息

    ```
    emitter.eventNames()
    emitter.listeners(eventName)
    emitter.listenerCount(eventName)
    ```

*   事件监听

    ```
    emitter.on(eventName, listener)
    emitter.once(eventName, listener)

    emitter.prependListener(eventName, listener)
    emitter.prependOnceListener(eventName, listener)

    emitter.addListener(eventName, listener)
    emitter.removeListener(eventName, listener)
    emitter.removeAllListeners([eventName])
    ```

*   事件触发

    ```
    emitter.emit(eventName[, ...args])
    ```

