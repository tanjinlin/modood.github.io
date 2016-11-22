# Ping++ 支付集成

## 基本设置

-   设置 api-key

    ```javascript
    var pingpp = require('pingpp')('sk_test_ibbTe5jLGCi5rzfH4OqPW9KC');
    ```

    参考配置：

    ```javascript
    var Promise = require('bluebird');

    var api_key = require('../../config/pingpp.js').api_key
    var pingpp = require('pingpp')(api_key);
    pingpp.setPrivateKeyPath(__dirname + '/../../config/pem/rsa_private_key.pem');

    Promise.promisifyAll(pingpp.charges.create)
    Promise.promisifyAll(pingpp.charges.createRefund)

    module.exports = pingpp;
    ```

## 验证签名设置

-   简介

    为了进一步增强交易请求的安全性，Ping++ 交易接口针对所有的 POST 和 PUT 请求已经新增 RSA
    加密验签功能。如果使用该签名验证功能，你需要生成密钥，然后将私钥配置到你的代码中，公钥上传
    至 Ping++ 管理平台并启用验签开关。

-   设置请求签名密钥：使用 API 的形式

    需要生成 RSA 签名(SHA256)并在请求头中添加 Pingplusplus-Signature

    关于如何生成 RSA 签名，请参考：[RSA 加密与解密](https://github.com/modood/modood.github.io/blob/master/blogs/rsa.md)

-   设置请求签名密钥：使用 SDK 的形式

    只需要配置私钥即可：

    ```javascript
    pingpp.setPrivateKeyPath(__dirname + "/rsa_private_key.pem");
    ```

-   上传公钥至 Ping++ 管理平台

    设置完代码中的私钥，你需要将已经生成的公钥(rsa_public_key.pem)填写到 Ping++ 管理平台上

    配置路径： 登录 Ping++ 管理平台->点击右上角公司名称->开发信息->商户公钥（用于商户身份验证）

## 支付过程

-   发起支付请求

    客户端请求服务器，服务器调用 Ping++ Server SDK 发起支付请求，发起请求所需参数具体可参考 API 文档。

-   获取支付凭据

    Ping++ 收到支付请求后返回给你的服务器一个 Charge 对象，这个 Charge 对象称为支付凭据。

-   将获得的支付凭据传给 Client

    服务器需要按照 JSON 字符串格式将支付凭据返回给你的客户端，Ping++ SDK 对此做了相应的处理，
    你只需要将获得的支付凭据直接传给客户端。客户端接收后使用该支付凭据用于调起支付控件

## Webhooks

-   接收 Webhooks 通知

    当用户完成交易后 Ping++ 会给你配置在 Ping++ 管理平台的 Webhooks 通知地址主动发送支付结果，
    我们称之为 Webhooks 通知。

    配置路径： 登录 Ping++ 管理平台->应用首页->技术开发->Webhooks

    Webhooks 通知是以 POST 形式发送的 JSON，放在请求的 body 里，内容是 Event 对象，
    支付成功的事件类型为 charge.succeeded ，你需要监听并接收 Webhooks 通知，
    接收到 Webhooks 后需要返回服务器状态码 2xx 表示接收成功，否则请返回状态码 500。

-   验证 Webhooks 签名

    Ping++ 的 Webhooks 通知包含了签名字段，可以使用该签名验证 Webhooks 通知的合法性。
    签名放置在 header 的自定义字段 x-pingplusplus-signature 中，签名用 RSA 私钥
    对 Webhooks 通知使用 RSA-SHA256 算法进行签名，以 base64 格式输出。

    Ping++ 在管理平台中提供了 RSA 公钥，供验证签名

    公钥具体获取路径：点击管理平台右上角公司名称->开发信息-> Ping++ 公钥。验证签名需要以下几步：

    ```
    1. 从 header 取出签名字段并对其进行 base64 解码。
    2. 获取 Webhooks 请求的原始数据。
    3. 将获取到的 Webhooks 通知、 Ping++ 管理平台提供的 RSA 公钥、和 base64 解码后的签名
       三者一同放入 RSA 的签名函数中进行非对称的签名运算，来判断签名是否验证通过。
    ```

    示例代码：

    ```javascript
    /* verify_pingxx_signature.js */
    var fs = require('fs');
    var crypto = require('crypto');

    var pingpp_rsa_public_key = fs.readFileSync(__dirname + '/../../config/pem/pingpp_rsa_public_key.pem', 'utf8');

    module.exports = function (raw_data, signature) {
      return crypto.createVerify('RSA-SHA256').update(raw_data, 'utf8').verify(pingpp_rsa_public_key, signature, 'base64');
    }
    ```
    ```javascript
    /* webhook_middleware.js */
    var verify_pingxx_signature = require('../utils/verify_pingxx_signature.js');

    var WebhookMiddleware = {};

    /**
     * 支付成功
     * @Author   https://github.com/modood
     * @DateTime 2016-04-13T17:15:31+0800
     */
    WebhookMiddleware.charge_succeeded = function (req, res, next) {
      if (!req.headers['x-pingplusplus-signature']) {
        return res.status(401).end('signature verification failed');
      }
      // 校验是不是来自 ping++ 的支付成功回调
      if (verify_pingxx_signature(JSON.stringify(req.body), req.headers['x-pingplusplus-signature'])) {
        next()
      } else {
        return res.status(401).end('signature verification failed');
      }
    }

    module.exports = WebhookMiddleware;
    ```

## 注意事项

> 1. 接收到 Webhooks 说明交易成功，交易失败不会发送 Webhooks ,未成功的交易结果直接在客户端返回。
> 2. 你需要在 Ping++ 的管理平台里填写 Webhooks 通知地址，详见 webhooks 配置说明，你的服务器需要监听这个地址并且接收 Webhooks 通知，接收到 Webhooks 通知后需给 Ping++ 返回服务器状态 2xx 。此时事件类型是 charge.succeeded，其字段 data 包含了 object 字段， object 字段的值是一个 Charge 对象。
> 3. 若你的服务器未正确返回 2xx，Ping++ 会在 25 小时内向商户服务器最多发送 8 次 Webhooks 通知，时间间隔分别为 2min、10min、10min、1h、2h、6h、15h，直到用户向 Ping++ 返回服务器状态 2xx 或者超过最大重发次数为止。
> 4. 你的服务器必须以 Ping++ 的 Webhooks 通知的结果作为交易结果，不可用客户端获得的结果作为支付成功与否的判断条件。
> 5. 如果没有收到 Webhooks 通知，可以调用 Ping++ 查询方法发起交易查询，该查询结果可以作为交易结果。

## 参考资料

官方文档：<https://www.pingxx.com/docs/server/charge>

