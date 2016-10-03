# JavaScript 前后端共用模块

目前，通行的Javascript模块规范共有两种：
[CommonJS](http://wiki.commonjs.org/wiki/Modules/1.1) 和
[AMD](https://github.com/amdjs/amdjs-api/wiki/AMD)

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

