# JavaScript 前后端共用模块

目前，流行的Javascript模块规范共有两种：
[CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1) 和
[AMD](https://github.com/amdjs/amdjs-api/wiki/AMD)

在一些同时需要 AMD 和 CommonJS 功能的项目中，你需要使用另一种规范：

Universal Module Definition（通用模块定义规范）。

[UMD](https://github.com/umdjs/umd) 创造了一种同时使用两种规范的方法，并且也支持全局变量定义。
所以UMD的模块可以同时在客户端和服务端使用。

示例代码：

```js
// AMD with global, Node, or global
;(function(root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD. Register as an anonymous module.
        define(function() {
            // Also create a global in case some scripts that are loaded
            // still are looking for a global even when an AMD loader is in use.
            return (root.something = factory());
        });
    } else if (typeof exports === 'object' && typeof module !== 'undefined') {
        // Node. Does not work with strict CommonJS, but only
        // CommonJS-like enviroments that support module.exports, like Node.
        module.exports = factory();
    } else {
        // Browser globals (root is self)
        root.something = factory();
    }
}(this, function() {
    var something = {}
    return something;
}));
```

# 参考

* [is.js](https://github.com/arasatasaygin/is.js/blob/master/is.js)
* [moment.js](https://github.com/moment/moment/blob/master/moment.js)
* [JavaScript 模块化入门Ⅰ：理解模块](https://zhuanlan.zhihu.com/p/22890374)

