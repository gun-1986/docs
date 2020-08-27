## 简介

> sed, 是Stream EDitor的简称，是非交互式命令行文本编辑器。

1. 完整命令格式
    ```
    sed OPTIONS... SCRIPT INPUTFILE...
    ```

    - 没有提供OPTIONS时，第一个非选项参数将作为第一个SCRIPT，随后的参数将作为INPUTFILE
        ```
        # 's/hello/world/' 是Script， input.txt是input file
        sed 's/hello/world/' input.txt
        ```
    - 多个输入文件将视为一个长流，除非使用`-s` 选项扭转这种行为
    - sed默认输出到标准输出，使用`-i` 选项才会直接编辑文件

2. 基本工作过程

    它读取输入流(可以是文件、标准输入)的每一行放进模式空间(pattern space)，同时将此行行号通过sed行号计数器记录在内存中，然后对模式空间中的行进行模式匹配，如果能匹配上则使用sed程序内部的命令进行处理，处理结束后，从模式空间中输出(默认)出去，并清空模式空间，随后再从输入流中读取下一行到模式空间中进行相同的操作，直到输入流中的所有行都处理完成。

    - 读取输入流的一行到模式空间，并记录行号。
    - 对模式空间中的内容进行匹配和处理。
    - 自动输出模式空间内容。
    - 清空模式空间内容。
    - 重复上述过程，直到所有行处理完成。


99. 参考

    - 手册： https://www.gnu.org/software/sed/manual/sed.html
    - https://pubs.opengroup.org/onlinepubs/7908799/xcu/sed.html
    - https://www.cnblogs.com/f-ck-need-u/p/7488469.html


## 命令选项
> 可以指定 多个 -e 和 -f选项。所有命令均以指定的顺序添加到脚本中。
1. **-n, --quiet, --silent**： 禁用自动打印，此时sed仅在通过p命令明确告知时才产生输出。
2. **-e script，--expression=script**： 添加脚本到sed命令集中
3. **-f script-file, --file=script-file**: 添加脚本文件到sed命令集中
4. **-i[SUFFIX], --in-place[=SUFFIX]**: 明确指定直接编辑文件
    - SUFFIX中不包含*，则备份文件名为`文件名+SUFFIX`
    - SUFFIX中包含`*`符号,`*`符号将被要编辑的文件名替换
5. **-E, -r, --regexp-extended**： 脚本中使用扩展正则表达式
6. **-s, --separate**： 多个输入文件时，默认将视为一个长流，使用`-s` 选项可扭转这种行为
7. **-u,--unbuffered**: 从输入文件加载最小数量的数据并更频繁地刷新输出缓冲区(对于输入来自  tail -f'，可以尽快开到转换后的输出)
8. **-z, --null-data**: 将输入的`nul字符(对应0x00)`视为行尾而不是`换行符\n(对应0x0a)`
    - 可以方便将行替换为其他字符,如将换行符替换为nul字符，如`sed -z -ibak 's|\x0a|\x00|g' file`

## sed脚本概述

> sed脚本由一个或多个的sed命令组成

## sed脚本中的命令
1. sed 命令遵循以下语法：`[addr]X[options]`
    - addr： addr是可选的行地址。如果addr指定，则仅在匹配的行上执行 命令X。[addr]可以是单个行号，正则表达式或行范围

        - 无addr `sed 's/hello/world/' input.txt > output.txt`,对所有行执行s替换命令
        - 单行号 `sed '144s/hello/world/' input.txt > output.txt`,仅对144行执行s替换命令
        - 行号范围 `sed '4,17s/hello/world/' input.txt > output.txt`，仅对4到17行执行s替换命令（`$`可以表示最后一行）
        - 步进范围：
            ```
            automation@watsng-ctrl-10-138-107-231:~$ seq 10 | sed '0~4s|^.*$|&&|g'
            1
            2
            3
            44
            5
            6
            7
            88
            9
            10
            ```
    - X：指单字母的sed命令
    - options: 与命令X相关的命令参数或选项

