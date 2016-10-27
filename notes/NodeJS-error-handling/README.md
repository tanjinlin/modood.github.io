# NodeJS 错误处理实践

## 错误和异常

错误和异常是有区别的：

1.  错误是Error的一个实例。
2.  错误被创建并且直接传递给另一个函数或者被抛出。
3.  如果一个错误被抛出了那么它就变成了一个异常。

错误分成两大类：

1.  操作失败

    正确编写的程序在运行时产生的错误。

2.  程序员失误

    程序里的Bug。这些错误往往可以通过修改代码避免。

## 错误的传递

三种传递错误的方式：

1.  作为异常 throw 抛出。
2.  把错误传给一个callback，这个函数正是为了处理异常和处理异步操作返回结果的。
3.  在EventEmitter上触发一个Error事件。

三种传递错误的方式的模式：

1.  throw以同步的方式传递异常。如果调用者（或者调用者的调用者）用了try/catch，则异常可以捕获。
    如果所有的调用者都没有用，那么程序通常情况下会崩溃（异常也可能会被domains或者进程级的uncaughtException捕捉到）。
    NodeJS 里的同步函数通常不会产生运行失败（主要的例外是类似于JSON.parse的用户输入验证函数）。

2.  Callback 是最基础的异步传递事件的一种方式。用户传进来一个函数（callback），之后当某个异步操作完成后调用这个 callback。
    通常 callback 会以callback(err,result)的形式被调用，这种情况下， err和 result必然有一个是非空的，取决于操作是成功还是失败。

3.  更复杂的情形是，当你在做一个可能会产生多个错误或多个结果的复杂操作的时候。比如，有一个请求一边从数据库取数据一边把数据发送回客户端，
    而不是等待所有的结果一起到达。在这个例子里，没有用 callback，而是返回了一个 EventEmitter，每个结果会触发一个row 事件，
    当所有结果发送完毕后会触发end事件，出现错误时会触发一个error事件。

## 函数指导原则

每个接口函数的文档都要很清晰的说明：

1.  预期参数，例如：ip
2.  参数的类型，例如：string
3.  参数的额外约束，例如：必须是有效的IP地址
4.  返回值
5.  调用者可能会遇到的操作失败
6.  怎么处理操作失败

示例：

```js
/**
 * Make a TCP connection to the given IPv4 address.  Arguments:
 *
 *    ip4addr        a string representing a valid IPv4 address
 *
 *    tcpPort        a positive integer representing a valid TCP port
 *
 *    timeout        a positive integer denoting the number of milliseconds
 *                   to wait for a response from the remote server before
 *                   considering the connection to have failed.
 *
 *    callback       invoked when the connection succeeds or fails.  Upon
 *                   success, callback is invoked as callback(null, socket),
 *                   where `socket` is a Node net.Socket object.  Upon failure,
 *                   callback is invoked as callback(err) instead.
 *
 * This function may fail for several reasons:
 *
 *    SystemError    For "connection refused" and "host unreachable" and other
 *                   errors returned by the connect(2) system call.  For these
 *                   errors, err.errno will be set to the actual errno symbolic
 *                   name.
 *
 *    TimeoutError   Emitted if "timeout" milliseconds elapse without
 *                   successfully completing the connection.
 *
 * All errors will have the conventional "remoteIp" and "remotePort" properties.
 * After any error, any socket that was created will be closed.
 */
function connect(ip4addr, tcpPort, timeout, callback) {
  assert.equal(typeof (ip4addr), 'string', "argument 'ip4addr' must be a string");
  assert.ok(net.isIPv4(ip4addr), "argument 'ip4addr' must be a valid IPv4 address");
  assert.equal(typeof (tcpPort), 'number', "argument 'tcpPort' must be a number");
  assert.ok(!isNaN(tcpPort) && tcpPort > 0 && tcpPort < 65536, "argument 'tcpPort' must be a positive integer between 1 and 65535");
  assert.equal(typeof (timeout), 'number', "argument 'timeout' must be a number");
  assert.ok(!isNaN(timeout) && timeout > 0, "argument 'timeout' must be a positive integer");
  assert.equal(typeof (callback), 'function');

  /* do work */
}
```

## 参考资料

* [NodeJS 错误处理最佳实践](http://www.kancloud.cn/thinkphp/nodejs-errorhandling/39145)

