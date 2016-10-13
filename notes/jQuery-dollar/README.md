# jQuery $ 符号的几点用途

$() 有如下用途：

1. 创建在 DOM 就绪后执行的代码
2. 通过包装集方法和选择和包装将要操作的 DOM 元素
3. 从 HTML 标记创建 DOM 元素
4. 为全局实用函数提供命名空间

## 文档就绪处理程序

-   传统形式

    ```javascript
    window.onload = function () {
      // code
    }
    ```
    注意： window 的 onload 机制只运行指定的一个函数，如果包含的任何第三方代码出于自身考虑
    使用 onload 机制，那这个限制可能导致难以发现的问题。

-   jQuery 正式形式

    ```javascript
    $(document).ready(function () {
      // code
    })
    ```

-   jQuery 简写形式

    ```javascript
    $(function () {
      // code
    })
    ```

## 包装集

-   从包装器获取元素

    $() 函数返回特殊的 javascript 对象，它包含与选择器相匹配的 DOM 元素数组，并拥有大量有用的
    预定义方法，可作用于已收集的元素集合。

    jQuery 的包装集方法有一个特点，执行完毕后会返回相同的一组元素，以便另一个操作做准备。

## 选择器

-   详细

    <http://docs.jquery.com/Selectors>

-   上下文

    $() 函数在接受选择器或者 HTML 代码作为第一个参数时，也接受了第二个参数（上下文）

    选择器作为第一个参数传递时，默认把 DOM 树的所有元素作为该选择器的上下文

    上下文参数可以是 DOM 元素的引用，也可以是包含 jQuery 选择器的字符串，或者是 DOM 元素包装集

-   基本 CSS 选择器

    可以通过元素的 id, class, 标签名以及页面中元素的 DOM 层级关系选择元素

    可以使用逗号操作符将多个选择器合并成一个选择器

## 创建 DOM 元素

-   创建

    可以通过向 $()函数传递一个包含 HTML 标记的字符串动态地创建 DOM 元素，例如：

    ```javascript
    $('<p>Hi there！</p>').insertAfter('#followMe');
    ```
    ```javascript
    $('<img>',{
      src: 'images/little.bear.png',
      alt: 'Little Bear',
      title:'I woof in your general direction',
      click: function(){
        alert($(this).attr('title'));
      }
    })
    .css({
      Styles the image
      cursor: 'pointer',
      border: '1px solid black',
      padding: '12px 12px 20px 12px',
      backgroundColor: 'white'
    })
    .appendTo('body');
    ```

-   常用方法

    attr , val , css , html , text , data , width , height , offset .

## 扩展 jQuery

-   扩展函数

    例如： 扩展一个 disable 函数用于禁用一组表单元素

    ```javascript
    $.fn.disable = function () {
      return this.each(function () {
        if (this.disabled !== null) {
          this.disabled = true;
        }
      })
    }
    ```

    $.fn.disable 表示使用 disabled 方法扩展 $ 包装集

    在函数内部 this 指向将要操作的 DOM 元素集合

    通过调用包装集上的 each() 方法遍历每一个匹配的元素

    在 each() 的迭代函数内 this 指向当前遍历的特定 DOM 元素

    调用函数：

    ```javascript
    $('#form#myForm input.special').disable().addClass('moreSpecial');
    ```

## 与其他库共存

-   noConflict

    调用 `jQuery.noConflict();` 就可以保留 $ 标识符给其他库使用了

    ```javascript
    jQuery.noConflict();
    (function($) {
      $(function() {
        // 使用 $ 作为 jQuery 别名的代码
      });
    })(jQuery);
    // 其他用 $ 作为别名的库的代码
    ```
