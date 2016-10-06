# 使用 scp 传输文件（基于 SSH）

## 简介

在 linux 下一般用 scp 这个命令来通过 ssh 传输文件。

> scp

> Secure copy

> Copy files between hosts using Secure Copy Protocol over SSH.

## 命令

```
usage: scp [-12346BCEpqrv] [-c cipher] [-F ssh_config] [-i identity_file]
           [-l limit] [-o ssh_option] [-P port] [-S program]
           [[user@]host1:]file1 ... [[user@]host2:]file2
```

## 常用

```
- Copy a local file to a remote host:
  scp local_file remote_host:/path/remote_file

- Copy a file from a remote host to a local folder:
  scp remote_host:/path/remote_file /path/local_dir

- Recursively copy the contents of a directory on a remote host to a local directory:
  scp -r /path/local_dir remote_host:/path/remote_dir

- Copy a file between two remote hosts transferring through the local host:
  scp -3 host1:/path/remote_file.ext host2:/path/remote_dir

- Use a specific username when connecting to the remote host:
  scp local_file remote_username@remote_host:/remote/path

- Use a specific ssh private key for authentication with the remote host:
  scp -i ~/.ssh/id_rsa local_file remote_host:/path/remote_file
```

## 示例

-   从服务器上下载文件

    ```
    scp root@192.168.1.101:/var/www/test.txt
    ```

-   上传本地文件到服务器

    ```
    scp /var/www/test.php  root@192.168.1.101:/var/www/
    ```

-   从服务器下载整个目录

    ```
    scp -r root@192.168.1.101:/var/www/test  /var/www/
    ```

-   上传目录到服务器
    ```
    scp -r test  root@192.168.1.101:/var/www/
    ```
