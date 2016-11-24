# net

*   net

    ```
    net.isIP(input)
    net.isIPv4(input)
    net.isIPv6(input)

    net.connect(options[, connectListener])
    net.connect(path[, connectListener])
    net.connect(port[, host][, connectListener])

    net.createConnection(options[, connectListener])
    net.createConnection(path[, connectListener])
    net.createConnection(port[, host][, connectListener])

    net.createServer([options][, connectionListener])
    ```

*   net.Server

    ```
    Events
      close
      connection
      error
      listening

    server.listening
    server.maxConnections

    server.ref()
    server.unref()

    server.address()
    server.getConnections(callback)
    server.close([callback])

    server.listen(handle[, backlog][, callback])
    server.listen(options[, callback])
    server.listen(path[, backlog][, callback])
    server.listen([port][, hostname][, backlog][, callback])
    ```

*   net.Socket

    ```
    new net.Socket([options])

    Events
      close
      connect
      data
      drain
      end
      error
      lookup
      timeout

    socket.bufferSize
    socket.bytesRead
    socket.bytesWritten
    socket.localAddress
    socket.localPort
    socket.remotePort
    socket.remoteAddress
    socket.remoteFamily
    socket.connecting
    socket.destroyed

    socket.ref()
    socket.unref()

    socket.pause()
    socket.resume()

    socket.connect(options[, connectListener])
    socket.connect(path[, connectListener])
    socket.connect(port[, host][, connectListener])

    socket.setNoDelay([noDelay])
    socket.setTimeout(timeout[, callback])
    socket.setEncoding([encoding])
    socket.setKeepAlive([enable][, initialDelay])
    socket.address()
    socket.destroy([exception])
    socket.write(data[, encoding][, callback])
    socket.end([data][, encoding])
    ```

