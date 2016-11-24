# cluster

*   cluster

    ```
    Events
      disconnect
      exit
      fork
      listening
      message
      online
      setup

    cluster.isMaster
    cluster.isWorker
    cluster.schedulingPolicy
    cluster.settings
    cluster.worker
    cluster.workers

    cluster.disconnect([callback])
    cluster.fork([env])
    cluster.setupMaster([settings])
    ```

*   Worker

    ```
    Events
      disconnect
      error
      exit
      listening
      message
      online

    worker.exitedAfterDisconnect
    worker.id
    worker.process

    worker.disconnect()
    worker.isConnected()
    worker.isDead()

    worker.kill([signal='SIGTERM'])
    worker.send(message[, sendHandle][, callback])
    ```

