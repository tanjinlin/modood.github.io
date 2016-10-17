# 使用 curl 基于 http 和 ftp 协议的上传和下载

## 下载

http:

`curl -C -O http://cgi2.tky.3wb.ne.jp/~zzh/screen1.JPG`

ftp:

`curl -u name:passwd ftp://ip:port/path/file`

`curl ftp://name:passwd@ip:port/path/file`

## 上传

http:

`curl -T localfile http://cgi2.tky.3web.ne.jp/~zzh/abc.cgi`

这时候，使用的协议是HTTP的PUT method

ftp:

`curl -T localfile -u name:passwd ftp://upload_site:port/path/`

## 表单提交

GET:

`curl http://www.yahoo.com/login.cgi?user=nickwolfe&password=12345`

GET模式什么option都不用，只需要把变量写在url里面就可以了

POST:

`curl -d "user=nickwolfe&password=12345" http://www.yahoo.com/login.cgi`

POST 请求文件上传：

``` HTML
<form method="POST" enctype="multipar/form-data" action="http://cgi2.tky.3web.ne.jp/~zzh/up_file.cgi">
  <input type=file name=upload>
  <input type=submit name=nick value="go">
</form>
```

这样一个HTTP表单，我们要用curl进行模拟，就该是这样的语法：

```
curl -F upload=@localfile -F nick=go http://cgi2.tky.3web.ne.jp/~zzh/up_file.cgi
```

## 其它参数

```
-i --include 把响应头输出出来
-X           指定 http 请求方式
```
