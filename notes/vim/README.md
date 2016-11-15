目录
*   [正常模式](#%E6%AD%A3%E5%B8%B8%E6%A8%A1%E5%BC%8F)
    * [移动光标](#%E7%A7%BB%E5%8A%A8%E5%85%89%E6%A0%87)
    * [增删改查](#%E5%A2%9E%E5%88%A0%E6%94%B9%E6%9F%A5)
    * [进入插入模式](#%E8%BF%9B%E5%85%A5%E6%8F%92%E5%85%A5%E6%A8%A1%E5%BC%8F)
    * [其他](#%E5%85%B6%E5%AE%83)
*   [命令模式](#%E5%91%BD%E4%BB%A4%E6%A8%A1%E5%BC%8F)
    * [移动光标](#%E7%A7%BB%E5%8A%A8%E5%85%89%E6%A0%87-1)
    * [查找与替换](#%E6%9F%A5%E6%89%BE%E4%B8%8E%E6%9B%BF%E6%8D%A2)
    * [保存和文件](#%E4%BF%9D%E5%AD%98%E5%92%8C%E6%96%87%E4%BB%B6)
    * [选项设置](#%E9%80%89%E9%A1%B9%E8%AE%BE%E7%BD%AE)
    * [Shell 命令](#shell-%E5%91%BD%E4%BB%A4)
*   [键盘映射](#%E9%94%AE%E7%9B%98%E6%98%A0%E5%B0%84)
    * [各种模式](#%E5%90%84%E7%A7%8D%E6%A8%A1%E5%BC%8F)
    * [不同模式下的键盘映射](#%E4%B8%8D%E5%90%8C%E6%A8%A1%E5%BC%8F%E4%B8%8B%E7%9A%84%E9%94%AE%E7%9B%98%E6%98%A0%E5%B0%84)
    * [键盘符号](#%E9%94%AE%E7%9B%98%E7%AC%A6%E5%8F%B7)
    * [定义快捷键](#%E5%AE%9A%E4%B9%89%E5%BF%AB%E6%8D%B7%E9%94%AE)
    * [其它功能](#%E5%85%B6%E5%AE%83%E5%8A%9F%E8%83%BD)

# 正常模式

## 移动光标

```
hjkl                          移动光标

w                             到下一个字的开头
b                             到上一个字的开头
e                             到下一个字的末尾

%                             匹配括号移动
*                             到下一个匹配单词
#                             到上一个匹配单词

0                             到本行行头
$                             到本行行尾

(                             前移 1 句
)                             后移 1 句
{                             前移 1 段
}                             后移 1 段

^                             到本行第一个非 blank 字符
g_                            到本行最后一个非 blank 字符

fx                            到下一个为 x 的字符处
tx                            到下一个为 x 的字符前

NG                            跳转到第 N 行
gg                            到第一行
G                             到最后一行

H                             当前屏幕最上行
M                             当前屏幕中间行
L                             当前屏幕最下行

zt                            将当前行移动到屏幕顶端
zz                            将当前行移动到屏幕中央
zb                            将当前行移动到屏幕底端
```

## 增删改查

```
u                             撤销
<C-r>                         重做

.                             重复上一个命令

dd                            剪切行
yy                            复制行
P                             粘贴到光标前面
p                             粘贴到光标后面

v                             可视化的选择

r                             替换一个字符
c                             修改（用于组合命令）

x                             删除一个字符
d                             删除（用于组合命令）

gU                            变大写
gu                            变小写
```

## 进入插入模式

```
i                             光标左侧
a                             光标右侧

I                             光标所在行开头
A                             光标所在行结尾

O                             光标上一行
o                             光标下一行

S                             删除光标所在行并进入插入模式
s                             删除光标所在的字符并进入插入模式
```

## 其它

```
K                             查找光标所在单词的手册
ZZ                            保存退出vi
ESC                           退出到正常模式
```

# 命令模式

## 移动光标

```
:n                            移动到第n行(.光标所在行、$末尾行)
:Sex                          水平分割一个窗口，浏览文件系统
:Vex                          垂直分割一个窗口，浏览文件系统
```

## 查找与替换

```
:/string                      正向查找
:?string                      反向查找
n                             查找下一个
:%s/old/new/g                 全局替换
:1,$ s/str1/str2/             用str2替换正文中首次出现的str1
:1,$ s/str1/str2/g            用str2替换正文中每次出现的str1
```

## 保存和文件

```
:w                            保存
:wq                           保存退出
:z                            保存退出
:q!                           不保存退出
:w [file]                     另存为
:a,bw [file]                  将第a行至第b行写入file文件
:r [file]                     读取fle文件的内容，插入当前光标所在行的后面
:e [file]                     编辑新文件
:f [file]                     重命名文件
:f                            输出当前文件名称和状态
:saveas <path/to/file>        另存为
:bn                           下一个文件
:bp                           上一个文件
:n                            下一个文件
:recover                      上次编辑意外退出，从临时文件恢复文件内容(该文件以.开头，并以.swp 结尾)
```

## 选项设置

```
:set autoindent               设置该选项，则正文自动缩进；
     ignorecase               设置该选项，则忽略规则表达式中大小写字母的区别；
     number                   设置该选项，则显示正文行号；
     ruler                    设置该选项，则在屏幕底部显示光标所在行、列的位置；
     tabstop                  设置按 Tab 键跳过的空格数。例如 :set tabstop=n，n 默认值为 8；
     mk                       将选项保存在当前目录的 .exrc 文件中；

:help <command>               显示相关命令的帮助。你也可以就输入 :help 而不跟命令。（退出帮助需要输入:q）
```

## Shell 命令

```
:![command]                   无需退出vi即可执行linux命令
:r !命令                       导入命令执行结果：
```

# 键盘映射

## 各种模式

-   常规模式(Normal)

    常规模式主要用来浏览和修改文本内容的

-   插入模式(Insert)

    插入模式则用来向文本中添加内容的

-   可视模式(Visual)

    可视模式相当于高亮选取文本后的普通模式

-   选择模式(Select)

    和可视模式不同的是，在这个模式下，选择完了高亮区域后，敲任何按键就直接输入并替换选择的文本了。

    普通模式下，可以按gh进入。

-   运算符模式(Operator Pending)

    用来接受命令的状态，这个状态在我们调用操作符（Operator）时被激活。

    常用到的Operator有d，y和c。例子：执行命令dw删除单词，这一模式就在d及w键之间短暂时间间隔内存在。

-   命令模式(Command)

    命令模式则多用于操作文件

## 不同模式下的键盘映射

| Command | Normal  | Visual  | Operator Pending | Insert Only | Command Line |
|:--------|:-------:|:-------:|:----------------:|:-----------:|:------------:|
| :map    | *       | *       | *                |             |              |
| :nmap   | *       |         |                  |             |              |
| :vmap   |         | *       |                  |             |              |
| :omap   |         |         | *                |             |              |
| :map!   |         |         |                  | *           | *            |
| :imap   |         |         |                  | *           |              |
| :cmap   |         |         |                  |             | *            |

提示： nore 表示非递归。例如：:noremap 和 :map 命令相对，作用模式和命令格式都相同。

## 键盘符号

详细： `:h key-notation`

```
<CR>            carriage return
<Return>        same as <CR>
<Enter>         same as <CR>

<Esc>           escape
<Tab>           tab
<Space>         space
<BS>            backspace

<Home>          home
<End>           end
<PageUp>        page-up
<PageDown>      page-down
<Up>            cursor-up
<Down>          cursor-down
<Left>          cursor-left
<Right>         cursor-right

<F1> - <F12>    function keys 1 to 12

<S-*>         shift-key
<C-*>         control-key
<M-*>         alt-key or meta-key
<A-*>         same as <M-*>
<D-*>         command-key (Macintosh only)
```

## 定义快捷键

-   自动补全括号引号

    ```
    inoremap ( ()<ESC>i
    inoremap [ []<ESC>i
    inoremap { {}<ESC>i
    inoremap < <><ESC>i
    inoremap " ""<ESC>i
    inoremap ' ''<ESC>i
    ```

-   利用Tab键和Shift-Tab键来缩进文本

    ```
    nmap <tab> V>
    nmap <s-tab> V<
    vmap <tab> >gv
    vmap <s-tab> <gv
    ```

## 其它功能

-   ab 与 map 的区别

    ab 可以将一长串字符用缩写来定义，

    map 可以将常用的很长的命令映射到一个新的功能键上。
