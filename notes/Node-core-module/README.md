# Node 核心模块学习

* [process](#process)
* [cluster](#cluster)
* [cryto](#cryto)
    * [hash](#hash)
    * [Hmac](#hmac)
    * [Cipher-Decipher](#cipher-decipher)
    * [Signer-Verify](#signer-verify)
* [child_process](#child_process)
* [https](#https)

## process

-   Exit Codes

    Node.js will normally exit with a 0 status code when no more async operations
    are pending.

-   Event

    `exit`: Emitted when the process is about to exit.

    `message`: Messages sent by `ChildProcess.send()`

    `beforeExit`

    `uncaughtException`

    `unhandledRejection`

    `rejectionHandled`

-   Signal Events

    Emitted when the processes receives a signal.

    [a list of standard POSIX signal](http://wikipedia.org/wiki/Unix_signal#POSIX_sign)

    for example：

    An easy way to send the SIGINT signal is with Control-C in most terminal programs.

    ```javascript
    // Start reading from stdin so we don't exit.
    process.stdin.resume();

    process.on('SIGINT', function() {
      console.log('Got SIGINT.  Press Control-D to exit.');
    });
    ```

## cluster

-   利用多核的优势

    现代的计算机CPU大多数都是多核的,但单个Node进程在运行时只能使用其中的一个内核。
    为了让单个程序使用多核实现起来更容易,Node增加了集群(cluster)API。

-   示例

    ```javascript
    var cluster = require('cluster');
    var http = require('http');
    var numCPUs = require('os').cpus().length;
    var workers = {};
    var requests = 0;
    if (cluster.isMaster) {
      for (var i = 0; i < numCPUs; i++) {
        workers[i] = cluster.fork();
        (function (i) {
          workers[i].on('message', function(message) {
            if (message.cmd == 'incrementRequestTotal') {
              requests++;
              for (var j = 0; j < numCPUs; j++) {
                workers[j].send({
                  cmd:
                  'updateOfRequestTotal',
                  requests: requests
                });
              }
            }
          });
        })(i);
      }
      cluster.on('death', function(worker) {
        console.log('Worker ' + worker.pid + ' died.');
      });
    } else {
      process.on('message', function(message) {
        if (message.cmd == 'updateOfRequestTotal') {
          requests = message.requests;
        }
      });
      http.Server(function(req, res) {
        res.writeHead(200);
        res.end('Worker ID ' + process.env.NODE_WORKER_ID
        + ' says cluster has responded to ' + requests
        + ' requests.');
        process.send({cmd: 'incrementRequestTotal'});
      }).listen(8000);
    }
    ```

## cryto

### hash

-   简介

    Hash，一般翻译做“散列”，也有直接音译为“哈希”的，就是把任意长度的输入（又叫做预映射， pre-image），
    通过散列算法，变换成固定长度的输出，该输出就是散列值。简单的说就是一种将任意长度的消息压缩到
    某一固定长度的消息摘要的函数。

    缺点：散列值的空间通常远小于输入的空间，不同的输入可能会散列成相同的输出，所以不可能从散列值来
    唯一的确定输入值。对不同的关键字可能得到同一散列地址，即key1≠key2，而f(key1)=f(key2)，这种现象称碰撞。

-   创建

    方法： `crypto.createHash(algorithm)`

    `algorithm` 参数可以指定加密算法，使用 `crypto.getHashes()` 方法可以查看支持的算法，
    使用 `openssl list-message-digest-algorithms` 命令也可以查看当前操作系统支持的算法。
    常用的为： `md5`, `sha1`, `sha256`, `sha512`

-   更新

    方法： `hash.update(data[, input_encoding])`

    `input_encoding` 参数可以指定编码，可以设置的编码类型： `utf8`, `ascii`, `binary`
    如果该参数未设置而 `data` 为字符串，则默认编码为 `utf8`，如果 `data` 为 `Buffer` 类型 ，
    则忽略该参数。

    `update` 方法可以调用多次，多次调用实际上是每次调用传入的数据相加。

-   消费

    方法： `hash.digest([encoding])`

    `encoding` 参数可以指定编码，可以设置的编码： `hex`, `binary`, `base64`，默认发回
    `Buffer` 类型 。

    一旦 ｀digest` 方法调用后， hash 对象将被清空不能再次使用。

-   示例

    Example: Using the hash.update() and hash.digest() methods:
    ```javascript
    const crypto = require('crypto');
    const hash = crypto.createHash('sha256');

    hash.update('some data to hash');
    console.log(hash.digest('hex'));
    ```

### Hmac

-   简介

    HMAC全名是 keyed-Hash Message Authentication Code，中文直译就是密钥相关的哈希运算
    消息认证码，HMAC运算利用哈希算法，以一个密钥和一个消息为输入，生成一个加密串作为输出。
    HMAC可以有效防止一些类似md5的彩虹表等攻击，比如一些常见的密码直接MD5存入数据库的，可能被反向破解。

-   创建

    方法： `crypto.createHmac(algorithm, key)`

-   更新

    方法： `hmac.update(data[, input_encoding])`

-   消费

    方法： `hmac.digest([encoding])`

-   示例

    Example: Using the hmac.update() and hmac.digest() methods:
    ```javascript
    const crypto = require('crypto');
    const hmac = crypto.createHmac('sha256', 'a secret');

    hmac.update('some data to hash');
    console.log(hmac.digest('hex'));
    ```

### Cipher-Decipher

-   简介

    对称加密，通信一方用KEK加密明文，另一方收到之后用同样的KEY来解密就可以得到明文。

-   创建

    方法： `crypto.createCipher(algorithm, password)`

    方法： `crypto.createDecipher(algorithm, password)`

    `algorithm` 参数可以指定加密算法，使用 `crypto.getCiphers()` 方法可以查看支持的算法，
    使用 `openssl list-cipher-algorithms` 命令也可以查看当前操作系统支持的算法。
    常用的为： `blowfish`, `aes192`

-   更新

    方法： `cipher.update(data[, input_encoding][, output_encoding])`

    方法： `decipher.update(data[, input_encoding][, output_encoding])`

    `input_encoding` 参数可以指定输入编码，可以设置的编码： `utf8`, `ascii`, `binary`，默认发回
    `Buffer` 类型 。

    `output_encoding` 参数可以指定输出编码，可以设置的编码： `hex`, `binary`, `base64`，默认发回
    `Buffer` 类型 。

    `update` 方法可以调用多次，直到 `final` 方法被调用。

-   结束

    方法： `cipher.final([output_encoding])`

    `final` 方法调用后 Cipher 对象将被清空，再调用 `update` 或 `final` 方法的话将抛出异常。

-   示例：加密

    Example: Using the cipher.update() and cipher.final() methods:
    ```javascript
    const crypto = require('crypto');
    const cipher = crypto.createCipher('aes192', 'a password');

    var encrypted = cipher.update('some clear text data', 'utf8', 'hex');
    encrypted += cipher.final('hex');
    console.log(encrypted);
    ```

-   示例：解密

    Example: Using the decipher.update() and decipher.final() methods:
    ```javascript
    const crypto = require('crypto');
    const decipher = crypto.createDecipher('aes192', 'a password');

    var encrypted = 'ca981be48e90867604588e75d04feabb63cc007a8f8ad89b10616ed84d815504';
    var decrypted = decipher.update(encrypted, 'hex', 'utf8');
    decrypted += decipher.final('utf8');
    console.log(decrypted);
    ```

### Signer-Verify

-   简介

    不对称加密算法，双方用不同的KEY加密和解密明文，通信双方都要有自己的公共密钥和私有密钥。
    公共密钥和私有密钥的特点是，经过其中任何一把加密过的明文，只能用另外一把才能够解开。

    公钥和私钥的生成参考: [RSA 加密与解密](https://github.com/modood/modood.github.io/blob/master/blogs/rsa.md)

-   创建

    方法： `crypto.createSign(algorithm)`

    方法： `crypto.createVerify(algorithm)`

    `algorithm` 参数可以指定加密算法，使用 `openssl list-public-key-algorithms`
    命令可以查看当前操作系统支持的算法。常用的为： `RSA-SHA256`

-   更新

    方法： `sign.update(data[, input_encoding])`

    方法： `verifier.update(data[, input_encoding])`

    `input_encoding` 参数可以指定输入编码，可以设置的编码： `utf8`, `ascii`, `binary`

-   生成签名

    方法： `sign.sign(private_key[, output_format])`

    `private_key` 参数指定加密使用的私钥

    `output_encoding` 参数可以指定输出编码，可以设置的编码： `hex`, `binary`, `base64`

    `sign` 方法返回值为生成的签名

-   签名校验

    方法： `verifier.verify(object, signature[, signature_format])`

    `object` 参数指定解密使用的公钥

    `signature` 参数可以指定签名

    `signature_format` 参数指定签名的编码： `hex`, `binary`, `base64`

    `verify` 方法返回值为布尔值

-   示例：生成签名

    Example: Using the sign.update() and sign.sign() methods:
    ```javascript
    /* get_signature.js */
    var fs = require('fs');
    var crypto = require('crypto');

    var rsa_private_key = fs.readFileSync(__dirname + '/../../config/pem/rsa_private_key.pem', 'utf8');

    module.exports = function (raw_data) {
      return crypto.createSign('RSA-SHA256').update(raw_data).sign(rsa_private_key, 'base64')
    }
    ```

-   示例：校验签名

    Example: Using the verify.update() and verify.verify() methods:
    ```javascript
    /* verify_signature.js */
    var fs = require('fs');
    var crypto = require('crypto');

    var rsa_public_key = fs.readFileSync(__dirname + '/../../config/pem/rsa_public_key.pem', 'utf8');

    module.exports = function (raw_data, signature) {
      return crypto.createVerify('RSA-SHA256').update(raw_data, 'utf8').verify(rsa_public_key, signature, 'base64');
    }
    ```

## child_process

-   Asynchronous Process Creation:

    用 cp.exec() 缓冲命令结果: `child_process.exec(command[, options], callback)`

    ```javascript
    var exec = require('child_process').exec,
        child;

    child = exec('cat *.js bad_file | wc -l',
      function (error, stdout, stderr) {
        console.log('stdout: ' + stdout);
        console.log('stderr: ' + stderr);
        if (error !== null) {
          console.log('exec error: ' + error);
        }
    });
    ```

    用 cp.spawn() 繁衍带有流接口的命令: `child_process.spawn(command[, args][, options])`

    这个函数跟 cp.exec() 不同，允许你跟每个子进程的 stdio 流交互

    ```javascript
    var cp = require('child_process');
    var child = cp.spawn('ls', [ '-l' ]);

    // stdout is a regular Stream instance, which emits 'data','end', etc.
    child.stdout.pipe(fs.createWriteStream('ls-result.txt'));

    child.on('exit', function (code, signal) {
      // emitted when the child process exits
    });
    ```

    用 cp.fork() 分散工作负载: `child_process.fork(modulePath[, args][, options])`

    cp.fork() 提供了 child.send() 和 child.on('message') 来向子进程发送和接受消息。
    在子进程中,你可以用 process.send() 和 process.on('message') 向父进程发送和接受消息。

-   Synchronous Process Creation：

    `child_process.spawnSync(command[, args][, options])`

    `child_process.execSync(command[, options])`

-   child-process-promise

    <https://github.com/patrick-steele-idem/child-process-promise>

## https

-   简介

    安全的超文本传输协议，提供了一种保证 Web 会话私密性的方法。将 HTTP 和 TLS/SSL 传输层
    结合到一起

-   私钥和公钥（证书）

    私钥用来解密客户端发往服务器的数据

    公钥（证书）用来加密从客户端发往服务器的数据

-   生成

    生成私钥使用 OpenSSL：

    `openssl genrsa 1024 > key.pem`

    生成公钥（证书）需要私钥：

    `openssl req -x509 -new -key key.pem > key-cert.pem`

-   应用

    ```javascript
    var https = require('https');
    var fs = require('fs');
    var options = {
      key: fs.readFileSync('./key.pem'),
      cert: fs.readFileSync('./key-cert.pem')
    };
    https.createServer(options, function (req, res) {
      res.writeHead(200);
      res.end("hello world\n");
    }).listen(3000);
    ```

-   目录遍历攻击

    <http://en.wikipedia.org/wiki/Directory_traversal_attack>
