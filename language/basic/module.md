# Module

## 描述

> 将程序的所有代码组织在一个文件中，随着程序越来越大，程序将很难维护。将文件拆分为多个文件，并有效组织起来，是Python中被称为Module和Package的工作


- 一个python文件就是一个模块，文件名 = 模块名 + ".py".如：

    文件名为`abc.py`,则其模块名为`abc`

    模块能定义函数，类和变量，模块里也能包含可执行的代码。

- A module is a file containing Python definitions and statements.


## 模块的查找路径

> 当一个spam模块被导入时的查找过程

1. 解释器首先查找带有spam名字的内置模块。
2. 在`sys.path`目录列表中查找名称为`spam.py`的文件。`sys.path`从以下位置初始化：

    - 包含输入脚本的目录
    - PYTHONPATH
    - 取决于安装的默认值

## 已编译的python文件

> 为了提示模块的加载速度，Python将每个模块的编译版本缓存在`__pycache_`_目录，名称形如`module.version.pyc`

1. 编译版本名称： 用cpython 3.3版本编译模块文件spam.py，将缓存到__pycache__/spam.cpython-33.pyc

2. 不用担心：
    - 自动检查源码修改日期，确定是否重新编译。
    - 编译后的模块与OS平台无关，可不同平台间共享


## `dir()`函数

> 内置函数dir()用于找出模块定义的名称

1. 带参数：列出对应模块定义的名称
    ```python
    import fibo, sys
    print(dir(sys))
    ```

2. 不带参数：列出当前定义的名称
    ```python
    a = '333'
    print(dir())

    # 输出
    ['__annotations__', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'a']
    ```

3. `dir()`没有列出内置函数和变量的名称，可通过以下方式列出
    ```python
    import builtins
    dir(builtins)

    # 输出
    ['ArithmeticError', 'AssertionError', 'AttributeError', 'BaseException',
    'BlockingIOError', 'BrokenPipeError', 'BufferError', 'BytesWarning',
    'ChildProcessError', 'ConnectionAbortedError', 'ConnectionError',
    'ConnectionRefusedError', 'ConnectionResetError', 'DeprecationWarning',
    'EOFError', 'Ellipsis', 'EnvironmentError', 'Exception', 'False',
    'FileExistsError', 'FileNotFoundError', 'FloatingPointError',
    'FutureWarning', 'GeneratorExit', 'IOError', 'ImportError',
    'ImportWarning', 'IndentationError', 'IndexError', 'InterruptedError',
    'IsADirectoryError', 'KeyError', 'KeyboardInterrupt', 'LookupError',
    'MemoryError', 'NameError', 'None', 'NotADirectoryError', 'NotImplemented',
    'NotImplementedError', 'OSError', 'OverflowError',
    'PendingDeprecationWarning', 'PermissionError', 'ProcessLookupError',
    'ReferenceError', 'ResourceWarning', 'RuntimeError', 'RuntimeWarning',
    'StopIteration', 'SyntaxError', 'SyntaxWarning', 'SystemError',
    'SystemExit', 'TabError', 'TimeoutError', 'True', 'TypeError',
    'UnboundLocalError', 'UnicodeDecodeError', 'UnicodeEncodeError',
    'UnicodeError', 'UnicodeTranslateError', 'UnicodeWarning', 'UserWarning',
    'ValueError', 'Warning', 'ZeroDivisionError', '_', '__build_class__',
    '__debug__', '__doc__', '__import__', '__name__', '__package__', 'abs',
    'all', 'any', 'ascii', 'bin', 'bool', 'bytearray', 'bytes', 'callable',
    'chr', 'classmethod', 'compile', 'complex', 'copyright', 'credits',
    'delattr', 'dict', 'dir', 'divmod', 'enumerate', 'eval', 'exec', 'exit',
    'filter', 'float', 'format', 'frozenset', 'getattr', 'globals', 'hasattr',
    'hash', 'help', 'hex', 'id', 'input', 'int', 'isinstance', 'issubclass',
    'iter', 'len', 'license', 'list', 'locals', 'map', 'max', 'memoryview',
    'min', 'next', 'object', 'oct', 'open', 'ord', 'pow', 'print', 'property',
    'quit', 'range', 'repr', 'reversed', 'round', 'set', 'setattr', 'slice',
    'sorted', 'staticmethod', 'str', 'sum', 'super', 'tuple', 'type', 'vars',
    'zip']
    ```


## 包

- 像文件系统目录一样，包是按层次结构组织的，并且包本身可能包含子包以及常规模块。可以将包视为文件系统上的目录，而将模块视为目录中的文件。但是不要从字面上看这样的类比，因为包和模块不需要源自文件系统。

    - 包只是一种特殊的模块（具体来说，任何包含__path__属性的模块都被视为包）

https://docs.python.org/3/reference/import.html#

非包模块： https://docs.python.org/3/reference/import.html#__path__
https://docs.python.org/3/whatsnew/3.3.html#pep-420-implicit-namespace-packages
