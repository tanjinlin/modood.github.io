# stream

*   stream.Writable

    ```
    new tream.Writable([options])

    Events
      close
      drain
      error
      finish
      pipe
      unpipe

    writable._write(chunk, encoding, callback)
    writable._writev(chunks, callback)
    writable.write(chunk[, encoding][, callback])
    writable.cork()
    writable.uncork()
    writable.end([chunk][, encoding][, callback])
    writable.setDefaultEncoding(encoding)
    ```

*   stream.Readable

    ```
    new stream.Readable([options])

    Events
      close
      data
      end
      error
      readable

    readable._read(size)
    readable.read([size])
    readable.isPaused()
    readable.setEncoding(encoding)
    readable.pause()
    readable.resume()
    readable.pipe(destination[, options])
    readable.unpipe([destination])
    readable.push(chunk[, encoding])
    readable.unshift(chunk)
    readable.wrap(stream)
    ```

*   stream.Duplex

    ```
    new stream.Duplex(options)

    stream.Transform
    stream.PassThrough
    ```

