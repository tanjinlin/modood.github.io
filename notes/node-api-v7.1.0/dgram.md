# dgram

*   dgram.Socket

    ```
    dgram.createSocket(type[, callback])
    dgram.createSocket(options[, callback])

    Events
      close
      error
      listening
      message

    socket.ref()
    socket.unref()

    socket.addMembership(multicastAddress[, multicastInterface])
    socket.dropMembership(multicastAddress[, multicastInterface])

    socket.send(msg, [offset, length,] port, address[, callback])

    socket.setTTL(ttl)
    socket.setMulticastTTL(ttl)
    socket.setMulticastLoopback(flag)
    socket.setBroadcast(flag)

    socket.address()

    socket.bind(options[, callback])
    socket.bind([port][, address][, callback])
    socket.close([callback])
    ```

