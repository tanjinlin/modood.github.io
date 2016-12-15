# OpenSSL 学习笔记

## 简介

OpenSSL 是 SSL/TLS 协议的开源实现程序，它由三部分组成：

```
libcrypto       通用加密库，提供各种加密函数
libssl          TLS/SSL协议的实现；基于会话实现了身份认证、数据机密性和会话完整性的TLS/SSL库
openssl         多用途命令行工具
```

## 命令

命令格式：

```
openssl command [ command_opts ] [command_args ]
```

子命令分为三类：

```
openssl list-standard-commands        标准命令
openssl list-message-digest-commands  消息摘要命令
openssl list-cipher-commands          加密命令
```

## 常用命令

```
enc                                   对称加密
dgst                                  单向加密
rand                                  生成随机数
passwd                                生成用户密码
genrsa                                生成私钥
rsa                                   提取公钥
req                                   生成证书签署请求(CSR文件)
x509                                  证书管理
pkcs12                                证书打包等
s_client                              SSL/TLS客户端程序
s_server                              SSL/TLS服务器端程序
```

