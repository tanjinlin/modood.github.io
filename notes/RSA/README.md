# NodeJS 签名生成和校验（基于RSA）

## RSA

![rsa](images/2016-07-12-11-43-33.png)

```
设若甲有一份需保密的数字商业合同发给乙签署。经过如下步骤：
1. 甲用乙的公钥对合同加密。
2. 密文从甲发送到乙。
3. 乙收到密文，并用自己的私钥对其解密。
4. 解密正确，经阅读，乙用自己的私钥对合同进行签署。
5. 乙用甲的公钥对已经签署的合同进行加密。
6. 乙将密文发给甲。
7. 甲用自己的私钥将已签署合同解密。
8. 解密正确，确认签署。
```

## Mac 下使用 openssl 生成 RSA 公钥和私钥

-   进入 openssl 交互环境

    ```
    $ openssl
    ```

-   生成 1024 位的 RSA 私钥

    ```
    $ genrsa -out rsa_private_key.pem 1024
    ```

    此时可以在当前路径下看到 rsa_private_key.pem 文件了。

    rsa_private_key.pem 文件示例：

    ```
    -----BEGIN RSA PRIVATE KEY-----
    MIICXQIBAAKBgQD2ncfROsnGE/75WxV36m9B4eZHsIr2jGJz7M/GP+GIpG7ggEUU
    IESA1soecvdUxFiV+1hV/qI6Qfito9vqZQSXmQViSCKGg1NRTeZLN1aNKUz9imk4
    1medeW4umMAOaxLvpIXDEzcdSO1lMn4IZ4Jui4u0ywfMAJE0fIrtgHZM2wIDAQAB
    AoGAfWQX9vA3K3l7SPng3onaa9saJRVEcrtKS7r6ochVOg6xOYC+ns8RRZjwR68Y
    xobWq9uSPJctkQV+FXudE36taA+i9a+nEFDfesmcxNV2XoRJjY42auCanZixBBil
    WcYAau0iGxYyj++Z9zU0SHzHL5WJPqpJxFjWY53K6wJseAECQQD+lb9eHwLcZaSE
    fWliwJHFeWhe9cJDAxbkeHIqgzQEKoLD1lzJxO6oIX3PI6STCJF5xlO3WMWMhQ+F
    NheH/kLbAkEA9/yxwJFloP+/P1Np22InvorQb2lgDs9fuoH/x2v1riO+STzRw6np
    KSIFDKK7V5cKEZCdDQrnhLp5iPGKIgU+AQJAfZfMd5de5vGxzra75b7QaxYw2h/t
    fPeqNH4C/FwLrj52kjxPPC7N+d3D3gtcZjjk46lmpV3C30bJWFNOGoXh3wJBALUb
    MN2H0gbQf+VJj8eOWaRIUIztEh/+xtS42AnWCGiS5gcqia8xyXwmwjVGKzd+sPW+
    /VNnIUnHvbaLX+wUlAECQQCim36cfBitLEh4bKNWxwDtJy+0Z3V2PAvCL8IopipF
    Qac3YpeB1+t9tw+pnP1rNXW/6Nl9FFyjgN0cLwFd9BFf
    -----END RSA PRIVATE KEY-----
    ```

-   生成 RSA 公钥

    ```
    $ rsa -in rsa_private_key.pem -pubout -out rsa_public_key.pem
    ```
    此时可以在当前路径下看到 rsa_public_key.pem 文件了。

    rsa_public_key.pem 文件示例：

    ```
    -----BEGIN PUBLIC KEY-----
    MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQD2ncfROsnGE/75WxV36m9B4eZH
    sIr2jGJz7M/GP+GIpG7ggEUUIESA1soecvdUxFiV+1hV/qI6Qfito9vqZQSXmQVi
    SCKGg1NRTeZLN1aNKUz9imk41medeW4umMAOaxLvpIXDEzcdSO1lMn4IZ4Jui4u0
    ywfMAJE0fIrtgHZM2wIDAQAB
    -----END PUBLIC KEY-----
    ```

-   PKCS8 格式的私钥

    某些编程语言需要 pkcs8 格式的公钥。使用 openssl 将刚才生成的私钥转为 PKCS8 格式：

    ```
    $ pkcs8 -topk8 -inform PEM -in rsa_private_key.pem -outform PEM –nocrypt
    ```

    把输出的内容复制粘贴进一个新的记事本中，可随便命名，只要知道这个是PKCS8格式的私钥即可。

    输出示例：

    ```
    -----BEGIN ENCRYPTED PRIVATE KEY-----
    MIICoTAbBgkqhkiG9w0BBQMwDgQIGQU42c9BuJoCAggABIICgP5tcVF5feRnq6Yu
    eix3kCQIAA7sBMybCh5eKbrwsBin4mi3LgMRZbvIZWnXvZ7Pn0F99P2QhpsAZ1N2
    rjOr1WXarRSCeI68oq27ckT/uSxqM9w6wWJAN3D501+WtSao1+seO/3qCZIlYE1Y
    71IRODBq6Lv/D9x6nWjPy/6kObNJOuvct/djdBTz/DxH4frQWq2XBVZtm3y3PV3M
    /1K8wo8gy+IZkC9XJFkWSm/ccGvIgfCmuqgPzUHlehMNZNnswts6dOUFbtQ+v/F5
    0jnfKXJSdHwgZY02ZmKrwQt3OsFR1+PuuxlHDmbdpALJzpSg2pjp/jPYbHG0Y35C
    R+BXdhyy9ZIcRpAiVe/Fttp1Txn35C0YnzdFY7pQTZcIlmYRtfSCLsYBjjD3NPAK
    5umW40h+CfNay2gl/4oIzmUOqp9NxCBZ6ojbCIdwS4z7aJZhIOG6h/XtLzXIQ/xw
    PoBnDqIUHLOCNp08fHZ2dIuDrMr0CxqdF4ORH5Q1eiUSOpYNg2HPwzcpSMpA6nRv
    29Ejh4se1kIbnTRtikFzrXm1Ocoup4hVsKxZIvccSRDDA0O9DdBcefysxoRBZjJu
    aBVGljzzNa3fAhjpZsXF1vOaGqx7cuwjofV/WYybcNXDUdTUwJlYvlvAn/IWSMfx
    t7asQSKjFYom+EF9jemYog6IEoz13HKJcgYbCSdqLvcvxuUsYPdKDuk9GHwackhR
    Qg+U8+s/9p8mNcz/1kds/FnD2gtlzjlX9ruJaxmNLQNW6DWv/mrE8XjI/dkvgY1N
    8LUpJqEXrkIN02JmstpIczvFJtOFheT3paKU1USwePS7tuIRRXbBEa/MAGCqfPY2
    5cxwIHg=
    -----END ENCRYPTED PRIVATE KEY-----
    ```

## NodeJS 生成并且检验 RSA 签名

-   生成签名

    ```js
    /* get_signature.js */
    var fs = require('fs');
    var path = require('path');
    var crypto = require('crypto');

    var rsa_private_key = fs.readFileSync(path.resolve(__dirname, '../config/pem/rsa_private_key.pem'), 'utf8');

    module.exports = function (raw_data) {
      return crypto.createSign('RSA-SHA256').update(raw_data, 'utf8').sign(rsa_private_key, 'base64')
    }
    ```

-   校验签名

    ```js
    /* verify_signature.js */
    var fs = require('fs');
    var path = require('path');
    var crypto = require('crypto');

    var rsa_public_key = fs.readFileSync(path.resolve(__dirname, '../config/pem/rsa_public_key.pem'), 'utf8');

    module.exports = function (raw_data, signature) {
      return crypto.createVerify('RSA-SHA256').update(raw_data, 'utf8').verify(rsa_public_key, signature, 'base64');
    }
    ```

## 参考资料

* [Node.js v4.6.0 Documentation Crypto](https://nodejs.org/dist/latest-v4.x/docs/api/crypto.html)
* [如何使用openssl生成RSA公钥和私钥对](http://blog.csdn.net/scape1989/article/details/18959657)
* [Nodejs 中常见的加密算法：MD5,RSA](http://blog.csdn.net/liudabaozhangxiaobei/article/details/51508592)
