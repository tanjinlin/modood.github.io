# NodeJS 图片上传到服务器并上传到七牛

## 前端 html 代码

```html
<form action="http://127.0.0.1:3000/v1/images" method="post" enctype="multipart/form-data">
  <span>选择要上传的图片：</span>
  <input type="file" name="nameOfFileInput" />
  <input type="submit" value="上传" />
</form>
```

## 路由和中间件（v1/images.js）

```javascript
var express = require('express');
var router = express.Router();

var multipart = require('connect-multiparty');
var multipartMiddleware = multipart({
  uploadDir: 'uploads/',
});

// 上传
router.post('/', multipartMiddleware, function (req, res, next) {
  var filepath = __dirname + '/../../' + req.files.nameOfFileInput.path

  require('../utils/upload_image.js')(filepath, function (err, data) {
    if (err) return res.api(null, {code: -1, msg: String(err)});
    return res.api({url: data.url })
  })
});

module.exports = router;
```

注意事项：

*   指定上传文件存放的目录（该目录需要提前创建好）
*   `req.files.nameOfFileInput.path` 中的 `nameOfFileInput` 必须和前端代码中
    的 file input 的 name 属性的值一致

## 上传到七牛（utils/upload_image.js）

```javascript
var fs = require('fs');

var qn = require('qn');

var client = qn.create({
  accessKey: '*****************************',
  secretKey: '*****************************',
  bucket: '*****************************',
  origin: '*****************************',
});

module.exports = function (filepath, callback) {
  var l = filepath.split('/');
  var filename = l[l.length-1];

  client.upload(fs.createReadStream(filepath), {key: filename}, function (err, data) {
    if (err) return callback(err);
    callback(null, data)
  });
}
```
