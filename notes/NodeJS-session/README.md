# NodeJS 中的 SESSION

## 简介

session 是另一种记录客户状态的机制，不同的是 cookie 保存在客户端浏览器中，而 session 保存在服务器上。

## cookie 和 session 的区别

cookie 和 session 的区别：

* cookie 数据存放在客户的浏览器上，session 数据放在服务器上。
* cookie 不是很安全，别人可以分析存放在本地的 cookie  并进行 cookie 欺骗，考虑到安全应当使用session。
* session 会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能，考虑到减轻服务器性能方面，应当使用 cookie。
* 单个 cookie 保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个 cookie。
* 建议将登陆信息等重要信息存放为 session ，其他信息如果需要保留，可以放在 cookie 中。

## express-session

安装：

```
$ npm install express-session
```

方法： `session(options)`，其中 options 中包含可选参数，主要有：

```
name        设置 cookie 中，保存 session 的字段名称，默认为 connect.sid 。
store       session 的存储方式，默认存放在内存中，也可以使用 redis，mongodb 等。express 生态中都有相应模块的支持。
secret      通过设置的 secret 字符串，来计算 hash 值并放在 cookie 中，使产生的 signedCookie 防篡改。
cookie      设置存放 session id 的 cookie 的相关选项，默认为 (default: { path: '/', httpOnly: true, secure: false, maxAge: null })
genid       产生一个新的 session_id 时，所使用的函数， 默认使用 uid2 这个 npm 包。
rolling     每个请求都重新设置一个 cookie，默认为 false。
resave      即使 session 没有被修改，也保存 session 值，默认为 true。
```

```javascript
var express = require('express');
var session = require('express-session');
var app = express();

app.use(session({
    secret: 'hello', //secret的值建议使用128个随机字符串
    cookie: {maxAge: 60 * 1000 * 30} // 过期时间（毫秒）
}));
app.get('/', function (req, res) {
    if (req.session.sign) {//检查用户是否已经登录
        console.log(req.session);//打印session的值
        res.send('welecome <strong>' + req.session.name + '</strong>, 欢迎你再次登录');
    } else {
        req.session.sign = true;
        req.session.name = 'Tom';
        res.send('欢迎登陆！');
    }
});
app.listen(80);
```

## 基于 Redis 管理 Session

安装：

```
$ npm install connect-redis
```

参数：

```
client      你可以复用现有的redis客户端对象， 由 redis.createClient() 创建
host        Redis服务器主机
port        Redis服务器端口
socket      Redis服务器的unix_socket
```

可选参数：

```
ttl         Redis session TTL 过期时间 （秒）
disableTTL  禁用设置的 TTL
db          使用第几个数据库
pass        Redis数据库的密码
prefix      数据表前辍即schema, 默认为 "sess:"
```

req在经过session中间件的时候就会自动完成session的有效性验证、延期/重新颁发、以及对session中数据的获取了。

```javascript
var express = require('express');
var session = require('express-session');
var RedisStore = require('connect-redis')(session);

var app = express();
var options = {
    "host": "127.0.0.1",
    "port": "6379",
    "ttl": 60 * 60 * 24 * 30,   //session的有效期为30天(秒)
};

// 此时req对象还没有session这个属性
app.use(session({
    store: new RedisStore(options),
    secret: 'express is powerful'
}));

app.listen(80);
```

