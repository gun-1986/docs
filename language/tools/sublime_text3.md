# Sublime Text 3

## 概述

  Sublime Text是一款流行的代码编辑器。（目前可永久试用，只是试用版不定期提示注册）

## 官方

- 官网：http://www.sublimetext.com/
- 帮助：http://www.sublimetext.com/support
- 参考：https://sublime-text-unofficial-documentation.readthedocs.io/en/latest/

## 安装

Windows下有两种风格的版本可用：安装版本和便携式版本

安装版本：下载安装文件安装

便携式版本：易移植，下载压缩文件解压即可

### Package Control

0. 描述

    Package Control是包管理工具，它使得包的查找，安装及更新更容易

1. 安装Package Control

    ctrl+shift+p：输入 install 后选择Package Control:Install Package,会自动安装Package Control.
后续插件都可以通过Package Control进行安装

2. 使用Package Control管理插件

* ctrl+shift+p，输入package，选择要进行的操作

    - 安装（Package Control:Install Package）：【注意】 已安装的软件不会被列出

    - 删除 (Package Control:Remove Package)

3. 常见问题

    出现下述问题，你可能需要更新channel (https://packagecontrol.io/channel_v3.json)
```
There are no packages available for installation
```


## Build System(构建系统)

0. 描述

    Sublime Text提供了构建系统，允许用户运行外部程序。

1. 配置

- 添加配置：Tools -> Build System -> New Build System...

```
// windowns中的Python3为例，配置如下，并保存为Python3.sublime-build
// ** selector：构建系统为Automatic，将通过selector来选择构建系统
// ** file_regex:Perl样式的正则表达式，用于捕获外部程序输出中的错误信息。
// ** cmd:构建系统实际执行的命令
{
"cmd": ["C:\\Program Files\\Python37\\python3.exe","$file"],
"file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
"selector": "source.python",
}

```

- 删除配置(未直接提供)

    可通过Preference -> Browse Packages...,找到刚配置对应的文件并删除
```
//删除 User目录下刚添加的Python3.sublime-build）
```

2. 使用(菜单Tools)

- 执行构建： F7 (或Ctrl+B)

- 取消构建：Ctrl+Break

- 使用指定构建系统：

    - 若Tools -> Build System 选择的是Automatic，构建时能自动选择构建系统，并记住选择，若想再切换构建系统时，选择Tools -> Build With...，重新选择构建系统并自动记住此次选择

99.帮助：

- http://www.sublimetext.com/docs/3/build_systems.html
- https://sublime-text-unofficial-documentation.readthedocs.io/en/latest/file_processing/build_systems.html

### SublimeCodeIntel 

0.描述

CodeIntel是一个代码智能引擎，已从Open Komodo Editor移植到一个独立的Python包中的，而SublimeCodeIntel插件提供了一个到CodeIntel的接口，使Sublime能智能代码补全


1.安装

关于SublimeCodeIntel安装，可能会遇到很多问题

- 额外安装：升级pip

    直接安装CodeIntel，可能会要求升级pip，如：You are using pip version 19.0.3, however version 20.0.2 is available.你可能需要强制升级才能成功（注意以管理员身份升级）
    ```
    # 升级命令
    python -m pip install --upgrade pip

    # 强制升级命令
    python -m pip install -U --force-reinstall pip
    ```
    

- 额外安装: VC++ build tools

    下载地址：https://download.microsoft.com/download/5/f/7/5f7acaeb-8363-451f-9425-68a90f98b238/visualcppbuildtools_full.exe

    直接安装CodeIntel，可能会有以下错误，使用上述下载文件完成相关安装即可。（参考 https://blog.csdn.net/u012247418/article/details/82314129 ）
```
error: Microsoft Visual C++ 14.0 is required. Get it with "Microsoft Visual
C++ Build Tools": http://landinghub.visualstudio.com/visual-cpp-build-tools
```
    也许可以从 https://visualstudio.microsoft.com/zh-hans/vs/older-downloads/?rr=https%3A%2F%2Fdocs.microsoft.com%2Fzh-cn%2Fvisualstudio%2Fproductinfo%2Fvs2015-sysrequirements-vs 
找到上述下载内容。

- 安装CodeIntel
```
pip3 install --upgrade --pre CodeIntel
```

- 安装SublimeCodeIntel

    下载地址（必须下载对应的版本，而不是最新的版本）：https://github.com/SublimeCodeIntel/SublimeCodeIntel/releases/tag/st3-v2.2.0
    
    下载后，将解压目录放置到 Preferences-> Browse Packages... 对应的目录即可

    注意：需要下载对应版本而不是最新版本（下载可能假成功，导致解压失败，我在换了台电脑后才成功了）

2.配置

- 配置Alt+鼠标右键返回：Preferences -> Package Settings -> SublimeCodeIntel -> Mouse Bindings - User
```
// 模仿SublimeCodeIntel的鼠标快捷键和键盘快捷键绑定
[
    { "button": "button2", "modifiers": ["alt"], "command": "back_to_python_definition", "press_command": "drag_select" }
]

```
    
3. 使用

- 手动提示和补全：快捷键 Ctrl + Shift + Space
- 跳转到定义： 右键 -> Jump to Symbol Definition  (快捷键: Alt+鼠标左键)
- 返回：右键 -> Back to Symbol Definition (快捷键: Alt+鼠标右键)

99.帮助：

https://github.com/SublimeCodeIntel/SublimeCodeIntel

### Ctags

0. 描述

Ctags可以为源文件的语言对象生成索引或tag文件，以允许这些对象能被编辑器或其他工具快速且容易的定位，Sublime中的Ctags支持使用Exuberant CTags生成的标签

1. 安装及配置

- 安装插件Ctags
- 下载Ctags可执行文件 https://sourceforge.net/projects/ctags/files/

2. 配置

- 让Ctags插件能找到Ctags可执行的二进制文件
```
//方法一：将配置中command指向Ctags指向文件 Preferences -> Package Settings -> Ctags -> Settings - User

{
    "command": "D:\\ctags58\\ctags.exe",
}

//方法二：将ctags.exe放置到环境变量Path对应的路径

```

- 配置跳转
```
//Ctrl+鼠标左键，跳转到定义
//Ctrl+鼠标右键，返回
[
    {
        "button": "button1",
        "count": 1,
        "press_command": "drag_select",
        "modifiers": ["ctrl"],
        "command": "navigate_to_definition"
    },
    {
        "button": "button2",
        "count": 1,
        "modifiers": ["ctrl"],
        "command": "jump_prev"
    }
]

```

- 重建标签，以便后续跳转或自动提示使用
```
目录右键 -> Ctags: Rebuild Tags
```

3. 使用

- 跳转到定义： 右键 -> Navigate to Definition  (快捷键: Ctrl+鼠标左键)
- 返回：右键 -> Jump Back (快捷键: Ctrl+鼠标右键)
 
99. 帮助

https://github.com/SublimeText/CTags

### Markdown相关插件

1. 安装插件

    * MarkdownEditing

    * MarkdownPreview


2. 设置：

    * 绑定快捷键 (Preferences -> Key Bindings)
```
[
    {
    "keys": ["alt+m"],
    "command": "markdown_preview",
    "args": {"target": "browser", "parser":"markdown"} },
]
```

    * 风格设置(View -> Syntax -> MarkdownEditing)
    
        - 支持3种风格：标准Markdown，GitHub风格的Markdown和MultiMarkdown,默认为GFM风格

    * 主题设置(GFM风格时：Preferences -> Package Settings -> Markdown Editing -> Markdown GFM Settings - User)
```
{

    "color_scheme": "Packages/MarkdownEditing/MarkdownEditor-Dark.tmTheme",

    // Layout
    "draw_centered": false,
    "word_wrap": true,
    "wrap_width": 180,
    "rulers": [],
}
```

3. 使用

    新建md后缀的文件后，Alt+m可以看到markdown文件的效果

4. 帮助：

    Preferences -> Package Settings -> Markdown Editing -> Readme

### SFTP插件相关

0. 描述

    通过FTP/SFTP连接远程服务器，进行远端和本地数据的同步，为远端编码等提供便利。

1. 安装

    - sftp

2. 配置

    File -> Open Folder -> 在空目录中点击右键 -> SFTP/FTP -> Maping to Remote...
    
    在新生成的sftp-config.json中根据实际情况修改配置，如保存时自动上传upload_on_save：
```
{
    save_before_upload": true,
    "upload_on_save": true,
    "sync_down_on_open": false,
    "sync_skip_deletes": false,
    "sync_same_age": true,
    "confirm_downloads": false,
    "confirm_sync": true,
    "confirm_overwrite_newer": false,
    
    "host": "192.168.5.67",
    "user": "automation",
    "password": "password",
    //"port": "22",
    
    "remote_path": "/home/automation/tmp/",
}
```

3. 操作

    - 从远端同步到本地：目录或文件右键 -> SFTP/FTP -> "Sync Remote -> Local..."

    - 从本地同步到远端：根据上述配置，保存时会自动同步到远端，或类上操作人工同步到远端

### 格式检查工具

0. 一些概念

lint或linter，是一种静态分析源代码以标记编程错误，bug，样式错误和可疑结构的工具

SublimeLinter是Sublime Text的插件，它提供了Linting代码的框架

SublimeLinter-flake8会使用SublimeLinter提供的接口，它需要使用flake8.exe工具

1.安装

- 额外安装：确保flask8安装在系统上（默认flake8.exe会放置在Python安装目录/Scripts下）
```
pip3 install flake8
```
- 安装SublimeLinter
- 安装SublimeLinter-flake8

2.配置

- 配置 Preferences -> Package Settings -> Settings
```
//设置安装的linter检查工具，设置行最大长度为100
// SublimeLinter Settings - User
{
    "linters": {
        "flake8": {
            "args": [
                "--max-line-length", "100",
                "--ignore", "E133,E226",
            ],
        }
    }

}
```


99. 帮助

- http://www.sublimelinter.com
- https://github.com/SublimeLinter/SublimeLinter
- https://github.com/SublimeLinter/SublimeLinter-flake8
- https://pypi.org/project/flake8/
- https://flake8.pycqa.org/en/latest/

### SublimeREPL

0. 描述

SublimeREPL可让您在常规编辑器选项卡中运行多种语言的交互式解释器。(它还允许通过telnet端口连接到正在运行的远程解释器)。

1. 安装

- 安装SublimeREPL，可能需要重启生效
    
2. 配置

- 添加快捷键，快速启动交互窗口每次打开交互窗口
```
// 绑定python交互窗口
// Preferences -> Keybindings 
{
    "keys": ["f5"],
    "command": "repl_open",
    "args": {"cmd": ["python", "-i", "-u"], "cwd": "$file_path", "encoding": "utf8", "extend_env": {"PYTHONIOENCODING": "utf-8"}, "external_id": "python", "syntax": "Packages/Python/Python.tmLanguage", "type": "subprocess"}
    }

// 绑定shell交互窗口（或windowns下cmd）
// Preferences -> Keybindings 
{
    "keys": ["f1"],
    "command": "repl_open",
    "args": {"cmd": {"linux": ["bash", "-i"], "osx": ["bash", "-i"], "windows": ["cmd.exe"]}, "cmd_postfix": "\n", "cwd": "$file_path", "encoding": {"linux": "utf-8", "osx": "utf-8", "windows": "$win_cmd_encoding"}, "env": {}, "external_id": "shell", "suppress_echo": true, "syntax": "Packages/Text/Plain text.tmLanguage", "type": "subprocess"}
    }
```

3. 使用

- 方法一： 菜单启动交互窗口
    - 打开：Tools -> SublimeREPL -> Python -> Python
    - 输入Python代码并交互执行

- 方法二： 使用配置的快捷键
```
{
    "keys": ["f5"],
    "command": "repl_open",
    "args": {"cmd": ["python", "-i", "-u"], "cwd": "$file_path", "encoding": "utf8", "extend_env": {"PYTHONIOENCODING": "utf-8"}, "external_id": "python", "syntax": "Packages/Python/Python.tmLanguage", "type": "subprocess"}
    }
```
    
99. 帮助

- https://sublimerepl.readthedocs.io/en/latest/
- 快捷键设置帮助： https://blog.csdn.net/sultry_yi/article/details/90613480
    + console命令：sublime.log_commands(True)

