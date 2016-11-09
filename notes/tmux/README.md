# Tmux 学习笔记

## 基础

官网

<https://tmux.github.io/>

简介

```
The tmux server manages clients, sessions, windows and panes. Clients are
attached to sessions to interact with them, either when they are created
with the new-session command, or later with the attach-session command.
Each session has one or more windows linked into it. Windows may be linked
to multiple sessions and are made up of one or more panes, each of which
contains a pseudo terminal.
```

默认前缀

````
Ctrl + b
```

## 安装

Ubuntu: `sudo apt-get install tmux`

Centos: `sudo yum install -y tmux`

Mac: `sudo brew install tmux`

## 命令

配置

```
tmux show-options -g        查看全局配置
tmux set -g prefix C-s      修改前缀
```

启动

```
start-server (alias: start)
```

关闭

```
kill-server
```

查看

```
list-sessions (alias: ls)
  [-F format]
```

新建

```
new-session (alias: new)
  [-AdDEP]
  [-c start-directory]
  [-F format]
  [-n window-name]
  [-s session-name]
  [-t target-session]
  [-x width]
  [-y height]
  [shell-command]
```

打开

```
attach-session (alias: attach)
  [-dEr]
  [-c working-directory]
  [-t target-session]
```

重命名

```
rename-session (alias: rename)
  [-t target-session] new-name
```

关闭

```
kill-session
  [-aC]
  [-t target-session]
```

## 快捷键

client

```
D   Choose a client to detach.
d   Detach the current client.
```

session

```
s   Select a new session for the attached client interactively.
$   Rename the current session.
L   Switch the attached client back to the last session.
(   Switch the attached client to the previous session.
)   Switch the attached client to the next session.
```

window

```
w   Choose the current window interactively.
0-9 Select windows 0 to 9.
c   Create a new window.
,   Rename the current window.
l   Move to the previously selected window.
p   Change to the previous window.
n   Change to the next window.
&   Kill the current window.
```

pane

```
%   Split the current pane into two, left and right.
"   Split the current pane into two, top and bottom.
;   Move to the previously active pane.
o   Select the next pane in the current window.
z   Toggle zoom state of the current pane.
x   Kill the current pane.
!   Break the current pane out of the window.
PageUp Enter       Copy mode and scroll one page up.
Up,Down,Left,Right Change to the pane above, below, to the left, or to the right of the current pane.
```

## 保存快照

[Tmux Resurrect](http://www.linuxidc.com/Linux/2015-07/120304.htm)
