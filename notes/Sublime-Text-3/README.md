# Sublime-Text-3 常用配置、插件、主题和配色方案

## 基础配置

-   [安装 Package Control](https://packagecontrol.io/installation)

    ```
    import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
    ```

-   编辑器配置

    ```js
    {
        // Encoding used when saving new files, and files opened with an undefined
        // encoding (e.g., plain ascii files). If a file is opened with a specific
        // encoding (either detected or given explicitly), this setting will be
        // ignored, and the file will be saved with the encoding it was opened
        // with.
        "default_encoding": "UTF-8",

        // Determines what character(s) are used to terminate each line in new files.
        // Valid values are 'system' (whatever the OS uses), 'windows' (CRLF) and
        // 'unix' (LF only).
        "default_line_ending": "unix",

        // Note that the font_face and font_size are overridden in the platform
        // specific settings file, for example, "Preferences (Linux).sublime-settings".
        // Because of this, setting them here will have no effect: you must set them
        // in your User File Preferences.
        "font_size": 10,

        // Columns in which to display vertical rulers
        "rulers": [80],

        // The number of spaces a tab is considered equal to
        "tab_size": 2,

        // Set to true to insert spaces when tab is pressed
        "translate_tabs_to_spaces": true,

        // Set to true to removing trailing white space on save
        "trim_trailing_white_space_on_save": false,

        // Set to true to ensure the last line of the file ends in a newline
        // character when saving
        "ensure_newline_at_eof_on_save": false,

        // Disables horizontal scrolling if enabled.
        // May be set to true, false, or "auto", where it will be disabled for
        // source code, and otherwise enabled.
        "word_wrap": "false",
    }
    ```

-   快捷键配置

    ```js
    [
      { "keys": ["alt+shift+f"], "command": "reindent" }
    ]
    ```

## 快捷键

-   常规

    | Windows/Ubuntu    |  Mac              | 描述 |   
    |:----------------- |:----------------: |:---- |
    | Alt + <n>         | ⌘<n>              | 选择相应标签页 |
    | F6                | F6                | 检测语法错误 |
    | F11               |                   | 全屏模式 |
    | Shift + F11       |                   | 全屏免打扰模式，只编辑当前文件 |
    | Ctrl + `          | ⌃ `               | python 控制台 |

-   移动

    | Windows/Ubuntu    |  Mac              | 描述 |   
    |:----------------- |:----------------: |:---- |
    | Ctrl + ←          | ⌘←                | 向左单位性地移动光标，快速移动光标。 |
    | Ctrl + →          | ⌘→                | 向右单位性地移动光标，快速移动光标。 |
    | Ctrl + G          | ⌃G                | : 跳转到相应的行 |
    | Ctrl + R          | ⌘R                | @ 快速列出/跳转到某个函数 |
    | Ctrl + P          | ⌘P                | 查找当前项目中的文件和快速搜索； 输入 @ 查找文件主标题/函数 输入 # 查找变量名 输入 : 跳转到文件某行 |
    | Ctrl + Shift + P  | ⇧⌘P               | 打开命令面板 |

-   选择

    | Windows/Ubuntu    |  Mac              | 描述 |   
    |:----------------- |:----------------: |:---- |
    | Ctrl + D          | ⌘D                | 选择词 (重复按下时多重选择相同的词进行多重编辑) |
    | Ctrl + L          | ⌘L                | 选择行 (重复按下将下一行加入选择) |
    | Ctrl + Shift + M  | ⌃⇧M               | 选择括号内的内容 |
    | Ctrl + Shift + L  | ⌃⇧L               | 选中多行后按下快捷键，即可同时编辑这些行 |

-   增加

    | Windows/Ubuntu    |  Mac              | 描述 |   
    |:----------------- |:----------------: |:---- |
    | Ctrl + Enter      | ⌘↩                | 在当前行后插入新行 |
    | Ctrl + Shift + D  | ⌃⇧D               | 复制光标所在整行，插入在该行之前 |

-   删除

    | Windows/Ubuntu    |  Mac              | 描述 |   
    |:----------------- |:----------------: |:---- |
    | Ctrl + KK         | ⌘KK               | 删除到行尾 |
    | Ctrl + X          | ⌘X                | 删除当前行 |

-   修改

    | Windows/Ubuntu    |  Mac              | 描述 |   
    |:----------------- |:----------------  |:---- |
    | Ctrl + J          | ⌘J                | 合并行 |
    | Ctrl + KU         | ⌘KU               | 改为大写 |
    | Ctrl + KL         | ⌘KL               | 改为小写 |
    | Ctrl + /          | ⌘/                | 注释当前行 |
    | Ctrl + Shift + ↑  | ⌃⌘↑               | 上移当前行 |
    | Ctrl + Shift + ↓  | ⌃⌘↓               | 下移当前行 |

## 常用插件

* [MarkdownPreview](https://github.com/revolunet/sublimetext-markdown-preview)：预览生成HTML的效果
* [MarkdownEditing](https://github.com/ttscoff/MarkdownEditing)：提供了Markdown格式的高亮编辑显示
* [PlainTasks](https://github.com/aziz/PlainTasks)：杰出的待办事项表
* [AutoFileName](https://github.com/BoundInCode/AutoFileName)：自动补全文件路径
* [AllAutocomplete](https://github.com/alienhard/SublimeAllAutocomplete)：基于已打开的文件补全代码
* [DocBlockr](https://github.com/spadgos/sublime-jsdocs)：编写代码注释的有效工具
* [GitGutter](https://github.com/jisaacks/GitGutter)：这些插件可以高亮相对于上次提交有所变动的行，换句话说是实时的diff工具。
* [Modific](https://github.com/gornostal/Modific)：这些插件可以高亮相对于上次提交有所变动的行，换句话说是实时的diff工具。
* [WebInspector](https://github.com/sokolovstas/SublimeWebInspector)：在 JavaScript调试方面，这是一个令人惊讶的工具
* [sublime_debugger](https://github.com/shuky19/sublime_debugger)：调试工具
* [Emmet](http://ipestov.com/the-best-plugins-for-sublime-text/)：快速编写 HTML/CSS 的编辑器中最流行的插件之一
* [Zen Coding](https://bitbucket.org/sublimator/sublime-2-zencoding)：Emmet 的前身
* [Git](https://github.com/kemayo/sublime-text-git)：使用编辑器直接和Git协同工作
* [Glue](https://github.com/chrissimpkins/glue)：会在界面下方显示一个小窗口，你可以在那里写Shell脚本。
* [BracketHighlighter](https://sublime.wbond.net/packages/BracketHighlighter)：打开/折叠代码，高亮匹配
* [ColorPicker](https://github.com/weslly/ColorPicker)：调色盘，写 CSS 非常方便
* [GutterColor](https://github.com/ggordan/GutterColor)：调色盘，写 CSS 非常方便
* [ColorHighlighter](https://github.com/Monnoroch/ColorHighlighter)：调色盘，写 CSS 非常方便
* [Inc-Dec-Value](https://github.com/rmaksim/Sublime-Text-2-Inc-Dec-Value)：增加或减少数字, 日期, 十六进制彩色值等等
* [Colorcoder](https://github.com/vprimachenko/Sublime-Colorcoder)：高亮所有变量
* [Vintage](https://github.com/sublimehq/Vintage)：支持 vi 编辑器的操作
* [ActualVim](https://github.com/lunixbochs/actualvim)：支持 vi 编辑器的操作
* [Alignment](https://github.com/wbond/sublime_alignment)：Package Control作者写的简单到极致的多行选择和多行选择对齐插件
* [Clipboard History](https://github.com/kemayo/sublime-text-2-clipboard-history)：粘贴板历史记录，方便使用复制/剪切的内容
* [SublimeLinter](https://github.com/kronuz/SublimeLinter)：一个支持lint语法的插件，可以高亮linter认为有错误的代码行
* [Nettuts-Fetch](https://github.com/weslly/Nettuts-Fetch)：可以自动更新一些开源库
* [JsMinifier](https://github.com/cgutierrez/JsMinifier)：该插件基于Google Closure compiler，自动压缩js文件。
* [ConvertToUTF8](http://www.sublimetext.com/forum/viewtopic.php?f=5&p=22274)：将文件编码从GBK转黄成UTF8，快捷键Ctrl+Shift+C

## 主题和配色方案

* 主题：<https://github.com/daylerees/colour-schemes>
* 配色方案：<http://colorsublime.com/>
* Soda：<http://buymeasoda.github.io/soda-theme/>
* Spacegray：<http://kkga.github.io/spacegray/>
* Flatland：<https://github.com/thinkpixellab/flatland>
* Tomorrow：<https://github.com/chriskempson/tomorrow-theme>
* Base 16：<https://github.com/chriskempson/base16>
* Solarized：<http://ethanschoonover.com/solarized>
* Predawn：<https://github.com/jamiewilson/predawn>
* itg.flat：<https://sublime.wbond.net/packages/Theme%20-%20itg.flat>

## 参考资料

* [Sublime Text 快捷键 Mac / Win](http://www.tuicool.com/articles/qaMnMz3)
* [Sublime Text 最佳插件列表](http://www.uis.cc/content-9-344-1.html)
* [一些必不可少的Sublime Text 2插件](http://www.qianduan.net/essential-to-sublime-the-text-2-plugins/)
