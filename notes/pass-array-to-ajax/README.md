# Ajax 传递数组参数

## 方法一：使用 traditional

-   简介

    ```
    traditional
    类型：Boolean
    Set this to true if you wish to use the traditional style of param serialization
    如果你想要用传统的方式来序列化数据，那么就设置为 true。
    ```

-   原理

    默认情况下，traditional 为 false，因为 jQuery 需要调用 jQuery.param 函数深度序列化参数对象，以适应如PHP和Ruby on Rails框架。

    例如 当提交的参数是数组 `{name:[value,value,value]}`, 则提交时会是"name[]=value&name[]=value"

    我们可以通过设置traditional 为true阻止深度序列化：

    ```
    $.ajax({
      type: "POST",
      url: "xxxxxxx",
      data: {
        arr: ['1', '2', '3']
      },
      traditional: true,
      success: function(data){
        console.log(data)
      }
    });
    ```

## 方法二：使用 JSON.stringify 和 JSON.parse 进行对参数对象序列化

-   简介

    ```
    JSON.stringify(value[, replacer [, space]])
    将任意的 JavaScript 值序列化成 JSON 字符串。

    JSON.parse(text[, reviver])
    将一个 JSON 字符串解析成为一个 JavaScript 值。在解析过程中，还可以选择性的修改某些属性的原始解析值。
    ```

-   文档

    [JSON.stringify()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)

    [JSON.parse()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)
