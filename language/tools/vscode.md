# vscode

>描述
    >> - Visual Studio Code是一个轻量级但功能强大的源代码编辑器
    >> - 内置支持JavaScript，TypeScript和Node.js
    >> - 有丰富的其他语言（例如C ++，C＃，Java，Python，PHP，Go）和运行时（例如.NET和Unity）扩展的生态系统

1. 下载

    zip格式免安装: https://code.visualstudio.com/Download#

2. 界面

    - 编辑区
    - 活动栏(Activity Bar),最左侧,可在Explorer(资源管理器),Search(查找),Source Control(git管理), Debug, Extensions多个视图间切换
    - 面板(Panel): 编辑区下方包含输出面板/调试信息面板/错误和警告面板/集成终端
    - 状态栏: 左下边栏可快速开关面板，右下边栏显示其他状态信息

3. 功能使用

    - 并排编辑： 编辑器右上角`Split Editor Right` Alt指向该按钮，可水平或垂直切换。(快捷键`Ctrl+\`)打开多个编辑窗口，并可通过拖动等实现水平或垂直方向打开多个编辑窗口
    - 代码大纲(minimap)：View -> Show Minimap
    - 命令面板（Command Palette）:可以通过命令访问VS code所有功能，快捷键`Ctrl + Shift + P`
    - 禅宗模式（Zen Mode）：隐藏除编辑器外的所有UI，使你可以专注于代码。快捷键`Ctrl + K Z`，指的是Ctrl+K，松开Ctrl，再按Z
    - 编辑器布局： View -> Editor Layout -> two columns

4. 常用快捷键
    - `Ctrl+P`:通过输入名称来打开文件
    - `Ctrl + Shift + P`: 打开命令面板(Command Palette),在命令面板中可以访问所有VS code 功能。
    - `Ctrl + Shift + O`: 导航到文件中特定符号，如函数或变量
    - `F12`: 转到定义
    -  `Alt + F12`: 偷看定义
    - `Alt + Left`: 导航回去
    - `Alt + Right`: 向前导航
    - `F5`: debug运行
    - `Ctrl + F5`: 直接运行
    - `Shift + F5`: 停止运行

5. 偏好设置
    - 偏好设置包含全局用户设置和工作空间设置
    - File -> Preferences -> Setting, 包含较为全面的设置。
        - 设置界面上方，可以过滤设置项，默认是分类的UI设置方式；
        - 其中右上角图标`Open Settings(JSON)` 可以以json格式打开配置文件及修改；
        - 每个设置项左侧可以对每个小项恢复缺省等操作。
    - 左下角`设置图标` -> Color Theme可以修改工作平台主题

6. 一些常用设置

    - 去除行位空格： "files.trimTrailingWhitespace": true
    - 现在打开编辑文档数量，以组为单位
    ```
    "workbench.editor.limit.enabled": true,
    "workbench.editor.limit.perEditorGroup": true,
    "workbench.editor.limit.value": 3
    ```

7. 打开终端

    - 打开终端： 右键文件，Open in Terminal.

99. 参考

    官网: https://code.visualstudio.com/
    其他：鼠标绑定尚不支持，不过可能不远了：https://github.com/microsoft/vscode/issues/3130

## Terminal
> vscode支持打开集成终端，以便快速执行需要的命令。终端位于编辑区下方的`TERMINAL面板`

1. 设置
    - 不同系统的缺省终端
        - Linux：环境变量SHELL
        - macOS：环境变量SHELL
        - Win10：PowerShell
        - Win7： cmd.exe

    - 切换缺省终端

        - 终端面板右上角`下拉列表`最下端有个`Select Default Shell`

2. 设置推荐终端：cmder
    > cmder 是一个增强型命令行工具。完整版可以使用windows，linux的命令，git命令，且无依赖拷贝即可用

    - 官网下载：https://cmder.net/
    - 解压到如`C:\cmder`
    - 设置cmder： `General -> Fonts`，disable以下选项，避免中文覆盖
    ```
        - Monospace
        - Compress long strings to fit space
    ```
    - 可以修改提示符：
        C:\cmder\vendor\clink.lua下的`local lambda = "λ"`中`λ`为`>`
    - 设置vscode的Terminal

    ```
    // ${fileDirname}是指文件最外层目录，可以写相对路径到内层目录如`code`

    "terminal.integrated.shell.windows": "C:\\Windows\\System32\\cmd.exe"
    "terminal.integrated.shellArgs.windows": ["/K", "C:\\cmder\\vendor\\init.bat"]
    "terminal.integrated.cwd": "${fileDirname}"
    ```

3. 使用

    - 终端面板右上角`+`可以快速打开缺省终端.(快捷键*Ctrl + Shift + \`*或菜单操作：`Terminal` ->`New Terminal`)
    - 终端面板右上角`Split图标`在右侧打开缺省终端
    - 切换终端：终端面板右上角`下拉列表`切换
    - 删除终端：`垃圾桶图标`可以关闭当前终端

99. 参考:
    - https://code.visualstudio.com/docs/editor/integrated-terminal
    - https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7
    - https://cmder.net/
    - https://github.com/cmderdev/cmder/blob/master/README.md

## snippets

0. 描述

    Code snippets 代码段，通过输入少量字符，智能补全一大段常用重复代码片段，能大量节省开发时间

1. 来源

    - 从市场上安装代码片段
    - 自定义代码段

2. 自定义代码段

    File -> Preferences -> User Snippets -> Global/


    - `HTTP client - json` 代码段的名字，没有description，智能提示时将用代码段的名称提示用户
    - `prefix` 代码段的提示前缀，输入列表中任意值，将能提示对应代码段
    - `body` 代码段的内容
        - 当代码段本身存在引号时，可能需要`\`转移
        - 制表符在代码段内的移动顺序为 `$1 -> $2 -> .. -> $varname ->$0`, shift+tab移动顺序与之相反
        - 缺省：`${1:foo}`，通过制表符移动但给一个缺省值
        - 选择：`${1|one,two,three|}`：通过制表符移动，提供若干可选择的内容
        - 变量：`$CURRENT_YEAR`,vscode提供了时间、注释及其他一些可用变量
    - `description` 匹配prefix内容时，IntelliSense显示的提示内容

    ```
    "HTTP client - json": {
		"prefix": ["http", "client", "json"],
		"body": [
			"pc$1.client.HTTP.url = f'http$3://{pc$2.interface.eth1.ip}/request_method'",
			"pc$1.client.HTTP.ignore_ssl = 'yes'",
			"pc$1.client.HTTP.method = 'POST'",
			"pc$1.client.HTTP.timeout = 20",
			"pc$1.client.HTTP.post_file = f'/watsng/scriptdata/{clean_json_file}'",
			"pc$1.client.HTTP.request_header_dict = {'Content-type': 'application/json'}",
			"pc$1.client.HTTP.response_all_list = ['200 OK']",
			"pc$1.client.HTTP.send()",
			"$0"
			],
			"description": "HTTP client - upload"
	},
    ```

99. 参考

    https://code.visualstudio.com/docs/editor/userdefinedsnippets

## markdown

0. 描述

    - Markdown 是一种轻量级标记语言，它使用易读易写的纯文本格式编写文档，并最终以HTML格式发布。

1. 使用(缺省支持)

    - 新建`.md`后缀的文件
    - 工作区右上角`Open preview to the Side`以便实时预览

## Python

1. 安装

    - 点击左侧`Extensions`(Ctrl+Shift+X)
    - 输入Python
    - 选择第一个安装(可以看到其发布者是Mircosoft并包含相关说明)
    - 上述安装完成后，实际只是安装了vscode相关的插件，其依赖的python包并没有安装。（一般在配置或使用时会提示用户安装）

2. 使用

    - IntelliSense(智能提示)：安装python后即能正常使用
    - debugging(调试器)：Debug -> Start Debugging(快捷键F5), 安装python后即能正常使用。

3. 配置

    - 切换解释器3种方法：
        - 状态条左侧会显示`当前选择的解释器`或`提示为设置解释器`
        - 命令面板输入：`Python: Select Interpreter`后选择
        - 设置pythonPath路径：
        ```
        "python.pythonPath": ".venv\\Scripts\\python.exe",
        ```

    - 虚拟环境的激活
        > 虚拟环境在运行python程序是会自动激活
        - Powershell: 由于策略限制，运行对应激活脚本`activate.ps1`失败，需修改策略如下：
            ```
            Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
            ```
        - 刚打开vscode时的终端可能并没有自动激活，即使新建终端也是如此
        - 执行一个python脚本是，会自动激活。此后新建终端也会自动激活

    - 添加查找路径PYTHONPATH： 工作目录 -> .vscode -> .env ================= 尚未正常工作
        ```
        PYTHONPATH=${workspaceFolder}/code/watchguard:${PYTHONPATH}
        ```
    https://code.visualstudio.com/docs/python/environments

### Python之REPL

0. 描述

    REPL，Read-Eval-Print-Loop，一种交互式解释器环境

1. 使用

    - 打开命令面板：View -> Command Palette...(快捷键 Ctrl+shift+P)
    - 输入Python,找到Start REPL


### Python之Interactive Window

0. 描述

    - 依赖Jupyter的有自动补全功能等的交互窗口。

1. 使用

    - 打开命令面板：View -> Command Palette...(快捷键 Ctrl+shift+P)
    - 打开Python: Show Python Interactive Window
    - 在交互窗口中输入python代码（已能自动补全），shift+Enter运行代码
    - 也可以以交互方式运行文件，通过使用Python: Run Current File in Python Interactive window


### Python之Linter

0. 描述

    - lint或linter，是一种静态分析源代码以标记编程错误，bug，样式错误和可疑结构的工具

1. 安装

    - `Ctrl + Shift + P`,输入Python，选择Select Linter, 选择flake8，右下侧会提示安装，选择Install

    - 根据安装过程中的警告信息，添加flake8的路径到path环境变量，并重启VS code

2. 配置

    - 设置限制长度为100： Settings -> Extensions -> Python 输入flake8搜索，在`python.linting.flake8`参数中Add Item: `--max-line-length=100`
    ```
    "python.linting.flake8Args": [
        "--max-line-length=100"
    ],
    "files.trimTrailingWhitespace": true,
    "python.linting.flake8Enabled": true
    ```
## SFTP

0. 描述

    将本地目录和远端目录进行人工或自动同步，避免过多人工同步带来的麻烦

1. 安装及配置

    - 安装：SFTP （一般选择下载数量标胶多的第一个进行安装）
    - 配置：File -> Open Folder打开一个空目录，Ctrl+Shift+P,输入"sftp config"，根据实际情况配置（最外层的空目录本身无法右键进行同步，需要在其内创建对应的子目录 ==> 子目录与remotePath目录下的子目录名字对应）
    ```
    {
        "name": "remote server",
        "host": "10.138.107.231",
        "protocol": "sftp",
        "port": 22,
        "username": "automation",
        "password":"******",
        "remotePath": "/",
        "uploadOnSave": true,
        "ignore": [
            ".vscode",
            ".git",
            ".DS_Store",
            ".pyc"
        ]
    }
```

2. 基本使用

    - 在空目录下创建remotePath子目录同名的子目录
    - 右键子目录：Sync Remote -> Local进行同步

3. 其他使用

    - SFTP: Open SSH on Terminal: 在VScode中打开sftp远端的终端。

99. 参考

-  https://github.com/liximomo/vscode-sftp


## Ctag

0. 描述

1. 使用

    - 制作tag ctags --tag-relative --extra=f -R .
    - Ctrl+鼠标左键：