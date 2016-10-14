# Connect/Express 的中间件机制

## 简介

在 Connect 中，中间件组件是一个 JavaScript 函数，它拦截 HTTP 服务器提供的请求和响应对象按惯例会接受三个参数：
一个请求对象，一个响应对象，还有一个通常命名为 next 的参数，它是一个回调函数，表明这个组件已经完成了它的工作，可以执行下一个中间件组件了。

## 注意

如果 next 不调用，控制权就不会被交回到分派器去调用下一个中间件组件，命令链中的后续中间件都不
会被调用，因此中间件的顺序也很重要。

## 挂载

挂载可以给中间件或整个程序定义一个路径前缀。

```javascript
connect()
  .use(logger)
  .use('/admin', restrict)
  .listen(3000);
```

## 创建可配置的中间件

可配置的中间件可以传入额外的参数来改变它的行为

例如：可配置的 Connect 中间件组件 logger

```javascript
function logger(format) {
  var regexp = /:(\w+)/g;
  return function (req, res, next) {
    var str = format.replace(regexp, function(match, property){
      return req[property];
    });
    console.log(str);
    next();
  }
}
module.exports = logger;
```
```javascript
connect()
  .use(logger(':method:url'))
```

## 错误处理中间件

错误处理中间件函数必须接受四个参数：err, req, res, next

```javascript
function errorHandler() {
  var env = process.env.NODE_ENV || 'development';
  return function(err, req, res, next) {
    res.statusCode = 500;
    switch (env) {
      case 'development':
        res.setHeader('Content-Type', 'application/json');
        res.end(JSON.stringify(err));
        break;
      default:
        res.end('Server error');
    }
  }
}
```
