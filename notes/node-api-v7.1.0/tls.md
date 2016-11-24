# tls

*   tls

    ```
    tls.connect(options[, callback])
    tls.connect(port[, host][, options][, callback])

    tls.getCiphers()
    tls.createSecureContext(options)
    tls.createServer(options[, secureConnectionListener])
    ```

*   tls.Server

    ```
    Events
      tlsClientError
      newSession
      OCSPRequest
      resumeSession
      secureConnection

    server.connections

    server.getTicketKeys()
    server.setTicketKeys(keys)
    server.addContext(hostname, context)
    server.address()

    server.listen(port[, hostname][, callback])
    server.close([callback])
    ```

*   tls.TLSSocket

    ```
    new tls.TLSSocket(socket[, options])

    Events
      OCSPResponse
      secureConnect

    tlsSocket.authorized
    tlsSocket.authorizationError

    tlsSocket.localAddress
    tlsSocket.localPort

    tlsSocket.encrypted

    tlsSocket.remoteAddress
    tlsSocket.remotePort
    tlsSocket.remoteFamily

    tlsSocket.renegotiate(options, callback)
    tlsSocket.setMaxSendFragment(size)

    tlsSocket.getCipher()
    tlsSocket.getEphemeralKeyInfo()
    tlsSocket.getPeerCertificate([ detailed ])
    tlsSocket.getProtocol()
    tlsSocket.getSession()
    tlsSocket.getTLSTicket()
    tlsSocket.address()
    ```

