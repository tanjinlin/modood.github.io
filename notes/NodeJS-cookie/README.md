# NodeJS 中的 COOKIE

## 基础

在 HTML 文档被发送之前，Web 服务器通过传送 HTTP 包头中的 Set-Cookie 消息把一个 cookie 发送到用户的浏览器中，如下示例：

```
Set-Cookie: name=value; Path=/; expires=Wednesday, 09-Nov-99 23:12:40 GMT;
```

其中比较重要的属性：

```
name=value         键值对，可以设置要保存的 Key/Value，注意这里的 name 不能和其他属性项的名字一样
Expires            过期时间（秒），在设置的某个时间点后该 Cookie 就会失效，如 expires=Wednesday, 09-Nov-99 23:12:40 GMT
maxAge             最大失效时间（毫秒），设置在多少后失效
secure             当 secure 值为 true 时，cookie 在 HTTP 中是无效，在 HTTPS 中才有效
Path               表示 cookie 影响到的路径，如 path=/。如果路径不能匹配时，浏览器则不发送这个Cookie
httpOnly           是微软对COOKIE做的扩展。如果在COOKIE中设置了“httpOnly”属性，则通过程序（JS脚本、applet等）将无法读取到COOKIE信息，防止XSS攻击产生
```

## NodeJS 中的 cookie

1.  使用 `response.writeHead`

    缺点：使用response.writeHead只能发送一次头部，即只能调用一次，且不能与response.render共存，否则会报错。

    ```javascript
    //设置过期时间为一分钟
    var today = new Date();
    var time = today.getTime() + 60*1000;
    var time2 = new Date(time);
    var timeObj = time2.toGMTString();
    response.writeHead({
       'Set-Cookie':'myCookie="type=ninja", "language=javascript";path="/";Expires='+timeObj+';httpOnly=true'
    });
    ```

2.  使用 `response.cookie`

    语法: `response.cookie('cookieName', 'name=value[name=value...]',[options]);`

    ```javascript
    response.cookie('haha', 'name1=value1&name2=value2', {maxAge:10 * 1000, path:'/', httpOnly:true});
    ```

## cookie-parser

express 在 4.x 版本之后，管理 session 和 cookies 等许多模块都不再直接包含在 express 中， 而是需要单独下载安装相应模块。

安装：

```
$ npm install cookie-parser
```

使用示例：

```javascript
var express      = require('express');
var cookieParser = require('cookie-parser');

var app = express();
app.use(cookieParser());

app.get('/', function (req, res) {
    // 如果请求中的 cookie 存在 isVisit, 则输出 cookie
    // 否则，设置 cookie 字段 isVisit, 并设置过期时间为1分钟
    if (req.cookies.isVisit) {
        console.log(req.cookies);
        res.send("再次欢迎访问");
    } else {
        res.cookie('isVisit', 1, {maxAge: 60 * 1000});
        res.send("欢迎第一次访问");
    }
});
app.listen(80);
```

