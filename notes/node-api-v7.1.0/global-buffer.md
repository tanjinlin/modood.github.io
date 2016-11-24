# buffer

## Buffer

*   分配

    ```
    Buffer.poolSize

    Buffer.from(array)
    Buffer.from(buffer)
    Buffer.from(string[, encoding])
    Buffer.from(arrayBuffer[, byteOffset[, length]])
    Buffer.alloc(size[, fill[, encoding]])
    Buffer.allocUnsafe(size)
    Buffer.allocUnsafeSlow(size)
    ```

*   其它

    ```
    Buffer.byteLength(string[, encoding])
    Buffer.compare(buf1, buf2)
    Buffer.concat(list[, totalLength])

    Buffer.isBuffer(obj)
    Buffer.isEncoding(encoding)
    ```

## buffer

需要使用 `const buffer = require('buffer')` 引入

*   属性

    ```
    buffer.INSPECT_MAX_BYTES
    buffer.kMaxLength
    ```

*   方法

    ```
    buffer.transcode(source, fromEnc, toEnc)
    ```

## Buffer 实例

*   输出和比较

    ```
    buf.length
    buf.toString([encoding[, start[, end]]])
    buf.toJSON()

    buf.equals(otherBuffer)
    buf.compare(target[, targetStart[, targetEnd[, sourceStart[, sourceEnd]]]])
    ```

*   查找和遍历

    ```
    buf[index]

    buf.includes(value[, byteOffset][, encoding])
    buf.indexOf(value[, byteOffset][, encoding])
    buf.lastIndexOf(value[, byteOffset][, encoding])

    buf.entries()
    buf.keys()
    buf.values()
    ```

*   修改

    ```
    buf.slice([start[, end]])
    buf.fill(value[, offset[, end]][, encoding])
    buf.copy(target[, targetStart[, sourceStart[, sourceEnd]]])

    buf.swap16()
    buf.swap32()
    buf.swap64()
    ```

*   读写

    ```
    buf.readIntBE(offset, byteLength[, noAssert])
    buf.readIntLE(offset, byteLength[, noAssert])
    buf.readInt8(offset[, noAssert])
    buf.readInt16BE(offset[, noAssert])
    buf.readInt16LE(offset[, noAssert])
    buf.readInt32BE(offset[, noAssert])
    buf.readInt32LE(offset[, noAssert])

    buf.readUIntBE(offset, byteLength[, noAssert])
    buf.readUIntLE(offset, byteLength[, noAssert])
    buf.readUInt8(offset[, noAssert])
    buf.readUInt16BE(offset[, noAssert])
    buf.readUInt16LE(offset[, noAssert])
    buf.readUInt32BE(offset[, noAssert])
    buf.readUInt32LE(offset[, noAssert])

    buf.readFloatBE(offset[, noAssert])
    buf.readFloatLE(offset[, noAssert])
    buf.readDoubleBE(offset[, noAssert])
    buf.readDoubleLE(offset[, noAssert])
    ```
    ```
    buf.write(string[, offset[, length]][, encoding])

    buf.writeIntBE(value, offset, byteLength[, noAssert])
    buf.writeIntLE(value, offset, byteLength[, noAssert])
    buf.writeInt8(value, offset[, noAssert])
    buf.writeInt16BE(value, offset[, noAssert])
    buf.writeInt16LE(value, offset[, noAssert])
    buf.writeInt32BE(value, offset[, noAssert])
    buf.writeInt32LE(value, offset[, noAssert])

    buf.writeUIntBE(value, offset, byteLength[, noAssert])
    buf.writeUIntLE(value, offset, byteLength[, noAssert])
    buf.writeUInt8(value, offset[, noAssert])
    buf.writeUInt16BE(value, offset[, noAssert])
    buf.writeUInt16LE(value, offset[, noAssert])
    buf.writeUInt32BE(value, offset[, noAssert])
    buf.writeUInt32LE(value, offset[, noAssert])

    buf.writeFloatBE(value, offset[, noAssert])
    buf.writeFloatLE(value, offset[, noAssert])
    buf.writeDoubleBE(value, offset[, noAssert])
    buf.writeDoubleLE(value, offset[, noAssert])
    ```

