# http

*   http

    ```
    http.METHODS
    http.STATUS_CODES

    http.globalAgent

    http.get(options[, callback])
    http.request(options[, callback])
    http.createServer([requestListener])
    ```

*   http.Server

    ```
    Events
      connect
      connection
      checkContinue
      checkExpectation
      clientError
      request
      upgrade
      close

    server.listening
    server.timeout
    server.maxHeadersCount

    server.setTimeout(msecs, callback)
    server.listen(path[, callback])
    server.listen(handle[, callback])
    server.listen([port][, hostname][, backlog][, callback])
    server.close([callback])
    ```

*   http.Agent

    ```
    new Agent([options])

    agent.requests
    agent.sockets
    agent.freeSockets
    agent.maxSockets
    agent.maxFreeSockets

    agent.getName(options)
    agent.createConnection(options[, callback])
    agent.destroy()
    ```

*   http.IncomingMessage

    ```
    Events
      aborted
      close

    message.httpVersion
    message.method
    message.url
    message.socket

    message.headers
    message.rawHeaders
    message.trailers
    message.rawTrailers

    message.statusCode
    message.statusMessage

    message.setTimeout(msecs, callback)
    message.destroy([error])
    ```

*   http.ClientRequest

    ```
    Events
      connect
      socket
      abort
      borted
      continue
      upgrade
      response

    request.abort()
    request.flushHeaders()

    request.setNoDelay([noDelay])
    request.setTimeout(timeout[, callback])
    request.setSocketKeepAlive([enable][, initialDelay])

    request.write(chunk[, encoding][, callback])
    request.end([data][, encoding][, callback])
    ```

*   http.ServerResponse

    ```
    Events
      close
      finish

    response.finished
    response.headersSent
    response.sendDate
    response.statusCode
    response.statusMessage

    response.setTimeout(msecs, callback)
    response.addTrailers(headers)

    response.getHeader(name)
    response.setHeader(name, value)
    response.removeHeader(name)

    response.write(chunk[, encoding][, callback])
    response.writeHead(statusCode[, statusMessage][, headers])
    response.writeContinue()
    response.end([data][, encoding][, callback])
    ```

