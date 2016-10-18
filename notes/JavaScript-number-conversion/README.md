# JavaScript 中 number 数据类型相关转换

## 浮点数取整

-   位运算

    两种符号 ~~ 和 |0

    原理： ~是按位取反的运算符，可以将浮点数通过舍去小数点后面的所有位来转换为整数。正整数可转换为
    无符号的十六进制值。然后再取反一次（~~）负负得正，就得到原来的整数。

    注意：如果需要做严格的四舍五入运算就要慎用此方法，那就还是得用 Math 函数。

-   parseInt

    丢弃小数部分,保留整数部分

-   Math.trunc (ES6)

    丢弃小数部分,保留整数部分

-   Math.ceil(), Math.floor(), Math.round()

    ```
    Math.ceil()         向上取整
    Math.floor()        向下取整
    Math.round()        四舍五入
    ```

## 字符串转换成数字

-   转换函数

    js提供了parseInt()和parseFloat()两个转换函数。前者把值转换成整数，后者把值转换成浮点数。
    只有对String类型调用这些方法，这两个函数才能正确运行；对其他类型返回的都是NaN(Not a Number)。

-   强制类型转换

    还可使用强制类型转换（type casting）处理转换值的类型。
    使用强制类型转换可以访问特定的值，即使它是另一种类型的。

    `Number(value)` ：把给定的值转换成数字（可以是整数或浮点数）；

-   利用js变量弱类型转换

    进行了算术运算，实现了字符串到数字的类型转换，不过这个方法还是不推荐的

    ```js
    var str= '012.345';
    var x = str - 0;
    var y = +str;
    var z = str * 1;
    ```

## 参考资料

* [js为什么不能正确处理小数运算？](http://m.jb51.net/article/77148.htm)
* [js 字符串转换成数字的三种方法](http://blog.csdn.net/ufo2910628/article/details/40735691)