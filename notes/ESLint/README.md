# ESLint 学习笔记

## [规则](http://eslint.cn/docs/rules/)

-   规则级别

    每条规则有 3 个等级：off、warn和error：

    * "off"   或 0 - 关闭规则
    * "warn"  或 1 - 开启规则，使用警告级别的错误：warn (不会导致程序退出)
    * "error" 或 2 - 开启规则，使用错误级别的错误：error (当被触发的时候，程序会退出)

-   参数

    有些规则还带有可选的参数，比如:

    ```js
    comma-dangle可以写成[ "error", "always-multiline" ]；
    no-multi-spaces可以写成[ "error", { exceptions: { "ImportDeclaration": true }}]。
    ```

-   临时禁用规则

    ```js
    // eslint-disable-next-line
    // eslint-enable
    // eslint-disable
    ```

## 参考资料

* [利用 ESLint 检查代码质量 - 老雷](http://morning.work/page/maintainable-nodejs/getting-started-with-eslint.html)
* [Configuring ESLint](http://eslint.cn/docs/user-guide/configuring)

