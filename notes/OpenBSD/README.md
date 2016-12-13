# OpenBSD 项目相关软件套件

## [OpenSSH](https://www.openssh.com/)

*   远程工具

    | 工具                            | 描述信息    |
    |:--------------------------------|:------------|
    | ssh                             | The basic rlogin/rsh-like client program
    | scp                             | File copy program that acts like rcp
    | sftp                            | FTP-like program that works over SSH1 and SSH2 protocol

*   密钥管理

    | 工具                            | 描述信息    |
    |:--------------------------------|:------------|
    | ssh-add                         | Tool which adds keys to in the above agent
    | ssh-keysign                     | Helper program for host-based authentication
    | ssh-keyscan                     | Utility for gathering public host keys from a number of hosts
    | ssh-keygen                      | Key generation tool

*   服务器端

    | 工具                            | 描述信息    |
    |:--------------------------------|:------------|
    | sshd                            | The daemon that permits you to log in
    | sftp-server                     | SFTP server subsystem (started automatically by sshd)
    | ssh-agent                       | An authentication agent that can store private keys

*   更多相关工具

    | 工具                            | 描述信息    |
    |:--------------------------------|:------------|
    | ssh-copy-id                     | use locally available keys to authorise logins on a remote machine

## [LibreSSL](https://www.libressl.org/)

*   工具

    | 工具                            | 描述信息    |
    |:--------------------------------|:------------|
    | openssl                         | The openssl utility, which provides tools for managing keys, certificates, etc.

*   类库

    | 工具                            | 描述信息    |
    |:--------------------------------|:------------|
    | libcrypto                       | a library of cryptography fundamentals
    | libssl                          | a TLS library, backwards-compatible with OpenSSL
    | libtls                          | a new TLS library, designed to make it easier to write foolproof applications

## 其它

### 网络相关

*   [OpenBGPD](http://www.openbgpd.org/)
*   [OpenNTPD](http://www.openntpd.org/)
*   [OpenSMTPD](https://www.opensmtpd.org/)

### 密钥交换

*   [OpenIKED](http://www.openiked.org/)

### 文档手册

*   [mandoc](http://mdocml.bsd.lv/)

