# zlib

*   zlib

    ```
    zlib.flush([kind], callback)
    zlib.params(level, strategy, callback)
    zlib.reset()
    ```

*   Unzip

    ```
    zlib.createUnzip(options)

    zlib.unzip(buf[, options], callback)
    zlib.unzipSync(buf[, options])
    ```

*   Gzip and Gunzip

    ```
    zlib.createGzip(options)

    zlib.gzip(buf[, options], callback)
    zlib.gzipSync(buf[, options])
    ```
    ```
    zlib.createGunzip(options)

    zlib.gunzip(buf[, options], callback)
    zlib.gunzipSync(buf[, options])
    ```

*   Deflate and Inflate

    ```
    zlib.createDeflate(options)

    zlib.deflate(buf[, options], callback)
    zlib.deflateSync(buf[, options])
    ```
    ```
    zlib.createInflate(options)

    zlib.inflate(buf[, options], callback)
    zlib.inflateSync(buf[, options])
    ```

*   DeflateRaw and InflateRaw

    ```
    zlib.createDeflateRaw(options)

    zlib.deflateRaw(buf[, options], callback)
    zlib.deflateRawSync(buf[, options])
    ```
    ```
    zlib.createInflateRaw(options)

    zlib.inflateRaw(buf[, options], callback)
    zlib.inflateRawSync(buf[, options])
    ```

