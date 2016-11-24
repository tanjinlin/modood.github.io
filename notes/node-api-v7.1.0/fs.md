# fs

*   常量

    ```
    fs.constants
    ```

*   流

    ```
    fs.createReadStream(path[, options])
    fs.createWriteStream(path[, options])
    ```

    fs.ReadStream
    ```
    Events
      open
      close

    readStream.bytesRead
    readStream.path
    ```

    fs.WriteStream
    ```
    Events
      open
      close

    writeStream.bytesWritten
    writeStream.path
    ```

*   文件状态

    ```
    fs.stat(path, callback)
    fs.statSync(path)
    fs.lstat(path, callback)
    fs.lstatSync(path)
    fs.fstat(fd, callback)
    fs.fstatSync(fd)
    ```

    fs.Stats
    ```
    stats.isFile()
    stats.isDirectory()
    stats.isBlockDevice()
    stats.isCharacterDevice()
    stats.isSymbolicLink() (only valid with fs.lstat())
    stats.isFIFO()
    stats.isSocket()
    ```

    ```
    fs.exists(path, callback)
    fs.existsSync(path)

    fs.realpath(path[, options], callback)
    fs.realpathSync(path[, options])

    fs.access(path[, mode], callback)
    fs.accessSync(path[, mode])

    fs.open(path, flags[, mode], callback)
    fs.openSync(path, flags[, mode])

    fs.close(fd, callback)
    fs.closeSync(fd)
    ```

*   文件监听

    ```
    fs.watch(filename[, options][, listener])
    fs.watchFile(filename[, options], listener)
    fs.unwatchFile(filename[, listener])
    ```

    fs.FSWatcher
    ```
    Events
      change
      error

    watcher.close()
    ```

*   文件读写

    ```
    fs.read(fd, buffer, offset, length, position, callback)
    fs.readSync(fd, buffer, offset, length, position)
    fs.readFile(file[, options], callback)
    fs.readFileSync(file[, options])
    fs.readlink(path[, options], callback)
    fs.readlinkSync(path[, options])
    fs.readdir(path[, options], callback)
    fs.readdirSync(path[, options])

    fs.write(fd, data[, position[, encoding]], callback)
    fs.write(fd, buffer, offset, length[, position], callback)
    fs.writeSync(fd, data[, position[, encoding]])
    fs.writeSync(fd, buffer, offset, length[, position])
    fs.writeFile(file, data[, options], callback)
    fs.writeFileSync(file, data[, options])

    fs.appendFile(file, data[, options], callback)
    fs.appendFileSync(file, data[, options])

    fs.truncate(path, len, callback)
    fs.truncateSync(path, len)
    fs.ftruncate(fd, len, callback)
    fs.ftruncateSync(fd, len)
    ```

*   权限管理

    ```
    fs.chmod(path, mode, callback)
    fs.chmodSync(path, mode)
    fs.lchmod(path, mode, callback)
    fs.lchmodSync(path, mode)
    fs.fchmod(fd, mode, callback)
    fs.fchmodSync(fd, mode)

    fs.chown(path, uid, gid, callback)
    fs.chownSync(path, uid, gid)
    fs.lchown(path, uid, gid, callback)
    fs.lchownSync(path, uid, gid)
    fs.fchown(fd, uid, gid, callback)
    fs.fchownSync(fd, uid, gid)
    ```

*   文件管理

    ```
    fs.utimes(path, atime, mtime, callback)
    fs.utimesSync(path, atime, mtime)
    fs.futimes(fd, atime, mtime, callback)
    fs.futimesSync(fd, atime, mtime)

    fs.rename(oldPath, newPath, callback)
    fs.renameSync(oldPath, newPath)

    fs.mkdir(path[, mode], callback)
    fs.mkdirSync(path[, mode])
    fs.mkdtemp(prefix[, options], callback)
    fs.mkdtempSync(prefix[, options])

    fs.rmdir(path, callback)
    fs.rmdirSync(path)
    ```

*   链接文件

    ```
    fs.symlink(target, path[, type], callback)
    fs.symlinkSync(target, path[, type])

    fs.link(existingPath, newPath, callback)
    fs.linkSync(existingPath, newPath)

    fs.unlink(path, callback)
    fs.unlinkSync(path)
    ```

*   磁盘同步

    ```
    fs.fsync(fd, callback)
    fs.fsyncSync(fd)

    fs.fdatasync(fd, callback)
    fs.fdatasyncSync(fd)
    ```

