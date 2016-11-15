* [全局函数或静态方法](#%E5%85%A8%E5%B1%80%E5%87%BD%E6%95%B0%E6%88%96%E9%9D%99%E6%80%81%E6%96%B9%E6%B3%95)
* [对象（Object）](#objectprototype)
* [函数（Function）](#functionprototype)
* [数组（Array）](#arrayprototype)
* [字符串（String）](#stringprototype)
* [数值（Number）](#numberprototype)
* [日期时间（Date）](#dateprototype)
* [正则表达式（RegExp）](#regexpprototype)
* [Promise](#promiseprototype)
* [Generator](#generatorprototype)

# 全局函数或静态方法

| 方法名称                 | 功能简介 |
|:------------------------|:--------|
| Object.create           | 创建一个拥有指定原型和若干个指定属性的对象
| Object.is               | 比较两个值是否严格相等
| Object.assign           | 将源对象（source）的所有可枚举属性，复制到目标对象（target）
| Array.from              | 将类似数组的对象（array-like object） 和可遍历（iterable）的对象转为真正的数组
| Array.of                | Array.of方法用于将一组值，转换为数组
| Number.isNaN            | 检测传入的值是否是 NaN。该方法比传统的全局函数 isNaN 更可靠，和全局函数 isNaN() 相比，该方法不会强制将参数转换成数字，只有在参数是真正的数字类型，且值为 NaN 的时候才会返回 true。
| Math.round              | 返回四舍五入后的整数
| Math.ceil               | 返回向上取整后的值
| Math.floor              | 返回小于x的最大整数
| Math.trunc              | 将数字的小数部分去掉，只留整数部分
| Math.max                | 返回 0 个到多个数值中最大值
| Math.min                | 返回 0 个到多个数值中最小值
| Math.random             | 返回 0 到 1 之间的伪随机数
| Date.now                | 返回自1970年1月1日 00:00:00 UTC到当前时间的毫秒数
| Date.parse              | 解析一个表示日期的字符串，并返回从 1970-1-1 00:00:00 所经过的毫秒数
| Date.UTC                | 接受和构造函数最长形式的参数相同的参数（从2到7），并返回从 1970-01-01 00:00:00 UTC 开始所经过的毫秒数
| JSON.parse              | 解析JSON字符串, 可以选择改变前面解析后的值及其属性，然后返回解析的值
| JSON.stringify          | 返回指定值的 JSON 字符串，可以自定义只包含某些特定的属性或替换属性值
| Promise.all             | 返回一个 promise，该 promise 会等 iterable 参数内的所有 promise 都被 resolve 后被 resolve， 或以第一个 promise 被 reject 的原因而 reject
| Promise.race            | 返回一个 promise，该 promise 会等 iterable 中的任意一个 promise 被解决或拒绝后，立刻以相同的解决值被解决或以相同的拒绝原因被拒绝。
| Promise.resolve         | 返回一个 promise 对象，这个 promise 对象是被解决后（resolved）的。
| Promise.reject          | 返回一个被拒绝的 Promise。使用是 Error 实例的 reason 对调试和选择性错误捕捉很有帮助。
| parseInt                | 将给定的字符串以指定基数（radix/base）解析成为整数或者 NaN，将截取整数部分。
| parseFloat              | 将参数中指定的字符串解析成为一个浮点数字并返回
| encodeURI               | 对统一资源标识符（URI）的组成部分进行编码的方法
| encodeURIComponent      | 对统一资源标识符（URI）的组成部分进行编码的方法
| decodeURI               | 用于解码由 encodeURI 方法或者其它类似方法编码的统一资源标识符（URI）
| decodeURIComponent      | 用于解码由 encodeURIComponent 方法或者其它类似方法编码的统一资源标识符（URI）

# Object.prototype

| 方法名称                 | 功能简介 |
|:------------------------|:--------|
| hasOwnProperty          | 判断某个对象是否含有指定的自身属性
| isPrototypeOf           | 测试一个对象是否存在于另一个对象的原型链上
| toString                | 返回一个代表该对象的字符串

# Function.prototype

| 方法名称                 | 功能简介 |
|:------------------------|:--------|
| apply                   | 在指定 this 值和参数（类数组对象）的的情况下调用某个函数
| call                    | 在指定 this 值和一组参数的的情况下调用某个函数
| bind                    | 创建一个 this 值绑定的新函数

# Array.prototype

| 方法名称                 | 功能简介 |
|:------------------------|:--------|
| concat                  | 将传入的数组或非数组值与原数组合并，组成一个新的数组并返回
| join                    | 将数组中的所有元素连接成一个字符串
| slice                   | 抽取当前数组中的一段元素组合成一个新数组
| splice                  | 用新元素替换旧元素，以此修改数组的内容
| includes                | 判断当前数组是否包含某指定的值，如果是返回 true，否则返回 false
| indexOf                 | 返回给定元素能找在数组中找到的第一个索引值，否则返回-1。
| lastIndexOf             | 返回给定元素能找在数组中找到的最后一个索引值，否则返回-1。
| forEach                 | 让数组的每一项都执行一次给定的函数，它总是返回 undefined
| map                     | 返回一个由原数组中的每个元素调用一个指定方法后的返回值组成的新数组
| filter                  | 测试数组的所有元素并创建一个包含所有通过测试的元素的新数组
| every                   | 测试数组的所有元素是否都通过了指定函数的测试
| some                    | 测试数组中的某些元素是否通过了指定函数的测试
| find                    | 如果数组中某个元素满足测试条件就会返回那个元素的值
| findIndex               | 如果数组中某个元素满足测试条件就会返回那个元素的索引
| reduce                  | 从左到右为每个数组元素执行一次回调函数，并把上次回调函数的返回值放在 一个暂存器中传给下次回调函数，并返回最后一次回调函数的返回值
| reduceRight             | 从右到左为每个数组元素执行一次回调函数，并把上次回调函数的返回值放在 一个暂存器中传给下次回调函数，并返回最后一次回调函数的返回值
| entries                 | 返回一个 Array Iterator 对象，该对象包含数组中每一个索引的键值对
| keys                    | 返回一个 Array Iterator 对象，该对象包含数组每个索引
| values                  | 返回一个 Array Iterator 对象，该对象包含数组每个索引的值

# String.prototype

| 方法名称                 | 功能简介 |
|:------------------------|:--------|
| concat                  | 将一个或多个字符串与原字符串连接合并，形成一个新的字符串并返回
| split                   | 通过把字符串分割成子字符串来把一个 String 对象分割成一个字符串数组
| slice                   | 提取字符串中的一部分，并返回这个新的字符串
| substr                  | 返回字符串中从指定位置开始到指定长度的子字符串
| substring               | 返回字符串两个索引之间（或到字符串末尾）的子串
| trim                    | 删除一个字符串两端的空白字符
| toLowerCase             | 将调用该方法的字符串值转为小写形式，并返回
| toUpperCase             | 将调用该方法的字符串值转为大写形式，并返回
| replace                 | 使用一个替换值（replacement）替换掉一个匹配模式（pattern）在原字符串中某些或所有的匹配项，并返回替换后的新的字符串
| match                   | 当字符串匹配到正则表达式（regular expression）时，match() 方法会提取匹配项
| includes                | 判断一个字符串是否被包含在另一个字符串中，如果是返回true，否则返回false
| startsWith              | 判断当前字符串是否是以另外一个给定的子字符串“开头”的，根据判断结果返回 true 或 false
| endsWith                | 判断当前字符串是否是以另外一个给定的子字符串“结尾”的，根据判断结果返回 true 或 false
| search                  | 执行一个查找，返回正则表达式在字符串中首次匹配项的索引。否则，返回 -1
| indexOf                 | 返回指定值在字符串对象中首次出现的位置，如果不存在，则返回 -1
| lastIndexOf             | 返回指定值在字符串对象中最后出现的位置，如果不存在，则返回 -1

# Number.prototype

| 方法名称                 | 功能简介 |
|:------------------------|:--------|
| toExponential           | 返回一个使用指数表示法表示的该数值的字符串表示
| toFixed                 | 返回一个使用定点表示法表示的该数值的字符串表示
| toPrecision             | 使用定点表示法或指数表示法来表示的指定显示位数的该数值对象的字符串表示

# Date.prototype

| 方法名称                 | 功能简介 |
|:------------------------|:--------|
| getTime                 | 返回一个时间的格林威治时间数值
| valueOf                 | 返回一个时间的格林威治时间数值
| getTimezoneOffset       | 返回协调世界时（UTC）相对于当前时区的时间差值，单位为分钟。
| toString                | 把一个日期转换为一个字符串，表示该Date对象。`Wed Sep 21 2016 15:22:55 GMT+0800 (CST)`
| toUTCString             | 把一个日期转换为一个字符串，使用UTC时区。`Wed, 21 Sep 2016 07:22:55 GMT`
| toISOString             | 方法返回一个 ISO（ISO 8601 Extended Format）格式的字符串，时区总是UTC（协调世界时），加一个后缀“Z”标识。`2016-09-21T07:22:55.461Z`

# RegExp.prototype

| 方法名称                 | 功能简介 |
|:------------------------|:--------|
| exec                    | 为指定的一段字符串执行搜索匹配操作。它的返回值是一个数组或者 null
| test                    | 执行一个检索，用来查看正则表达式与指定的字符串是否匹配。返回 true 或 false。

# Promise.prototype

| 方法名称                 | 功能简介 |
|:------------------------|:--------|
| then                    | 添加肯定和否定回调到当前 promise, 返回一个新的 promise, 将以回调的返回值来 resolve
| catch                   | 只处理Promise被拒绝的情况，并返回一个Promise。

# Generator.prototype

| 方法名称                 | 功能简介 |
|:------------------------|:--------|
| next                    | 返回一个包含属性 done 和 value 的对象. 该方法也可以通过接受一个参数用以向生成器传值
| return                  | 返回给定的值并结束生成器。
| throw                   | 向生成器抛出异常，并恢复生成器的执行，返回带有 done 及 value 两个属性的对象。
