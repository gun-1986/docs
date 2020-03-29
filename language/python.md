# python

1. 一些概念
    - PEP: Python增强建议，是the Python Enhancement Proposals的简写

99. 参考

    https://www.python.org/dev/peps/

## Virtualenv
> virtualenv是用于创建隔离的Python环境的工具。从Python开始3.3，它的一个子集已集成到venv模块下的标准库中.

> **注意**：虚拟环境并非设计为可移植的,尽管个人也认为这有些不妥，但官方似乎并不认为它是一个bug。而且，要包括pip等可移植，实际修改也并非仅描述中提及的一个地方就可以了。参见：https://bugs.python.org/issue36964

1. 安装virtualenv

    `pip install virtualenv`

2. 创建虚拟环境

    - 创建虚拟环境的命令：`virtualenv venvpath` 或 `python3 -m venv venvpath`

        - 可能用到的参数：`--system-site-packages` 允许虚拟环境使用系统的包
        - 默认虚拟环境安装后，会包含`seed packages(种子包):pip, setuptools, wheel`，以便扩展

3. 使用虚拟环境
    - 直接使用：pip等工具包含绝对路径，安卓包的位置能正确放置： `venvpath\Scripts\python.exe` 直接 `venvpath\Scripts\pip.exe`
    - 切换到虚拟环境使用：其原理是执行批处理时，会修改相关的环境变量，让命令python和pip等均指向当前的虚拟环境。（并不会对系统环境有影响，只是在相应命令行中切换环境。）
        - 命令行激活虚拟环境：`venvpath\Scripts\activate.bat`
        - 命令行停止虚拟环境：`venvpath\Scripts\deactivate.bat`

99. 参考

    - https://docs.python.org/3/library/venv.html
    - https://www.python.org/dev/peps/pep-0405/
    - https://virtualenv.pypa.io/en/latest/

## pip

>  pip是python包的安装工具,是the package installer for Python的简写。

1. 安装pip及升级
    > pip大多在安装python时已经安装

    - 下载get-pip.py源码： curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
    - 执行get-pip.py: python get-pip.py
    - 升级命令`python -m pip install --upgrade pip`
    - 强制升级命令`python -m pip install -U --force-reinstall pip`

2. 基本使用

    > 基本使用线路图：pip search -> pip install/download -> pip freeze/list ->pip uninstall

    - pip支持从PyPI，版本控制，本地项目以及直接从分发文件进行安装。
    - 事例之快速安装另一PC上安装的所有python包
        - 生成`需求文件`(包含已安装的文件列表)：`pip freeze > requirements.txt`
        - 从需求文件安装:`pip install -r requirements.txt`

3. 加速安装之使用国内镜像
    > pip安装库文件时，默认使用国外的源文件,使用国内镜像站点可以提升安装速度

    - 临时使用命令，如：pip install panda -i http://mirrors.aliyun.com/pypi/simple/  --trusted-host mirrors.aliyun.com

        - （1）阿里云 http://mirrors.aliyun.com/pypi/simple/
        - （2）豆瓣 http://pypi.douban.com/simple/
        - （3）清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/
        - （4）中国科学技术大学 http://pypi.mirrors.ustc.edu.cn/simple/
        - （5）华中科技大学 http://pypi.hustunique.com/
    - 永久修改：在用户目录(如xxx)创建相应的pip目录和pip.ini文件，如C:\Users\xxx\pip\pip.ini，内容如下：

        ```
        [global]
        index-url = http://mirrors.aliyun.com/pypi/simple/
        [install]
        trusted-host = mirrors.aliyun.com
        ```

99. 参考
    - https://pip.pypa.io/en/stable/installing/
    - https://pypi.org/project/pip/
    - https://pip.pypa.io/en/stable/user_guide/#
    - https://blog.csdn.net/sinat_21591675/article/details/82770360
