# sedsed

## 简介

sedsed 可以对sed脚本进行调试,是sed学习和debug的绝佳工具。

## 安装

    ```
    sudo pip3 install sedsed
    sudo cp /usr/local/bin/sedsed /usr/bin/
    ```

## 使用事例


1. debug sed命令
    - 测试文件`file`内容
        ```
        1
        2
        3
        ppp
        1
        2
        3
        zzz
        1
        2
        3
        ```

    - 实际命令输出
        ```
        automation@watsng-ctrl-10-138-107-231:~$ sed -e '/ppp/i iii' -e '/zzz/a aaa' file
        1
        2
        3
        iii
        ppp
        1
        2
        3
        zzz
        aaa
        1
        2
        3

        ```

    - debug sed输出：
        - PATT
        - HOLD
        - COMM
        - 无标识：

        ```
        automation@watsng-ctrl-10-138-107-231:~$ sedsed -d -e '/ppp/i iii/' -e '/zzz/a aaa' file
        PATT:1$
        HOLD:$
        COMM:/ppp/ i\\Niii/
        PATT:1$
        HOLD:$
        COMM:/zzz/ a\\Naaa
        PATT:1$
        HOLD:$
        1
        PATT:2$
        HOLD:$
        COMM:/ppp/ i\\Niii/
        PATT:2$
        HOLD:$
        COMM:/zzz/ a\\Naaa
        PATT:2$
        HOLD:$
        2
        PATT:3$
        HOLD:$
        COMM:/ppp/ i\\Niii/
        PATT:3$
        HOLD:$
        COMM:/zzz/ a\\Naaa
        PATT:3$
        HOLD:$
        3
        PATT:ppp$
        HOLD:$
        COMM:/ppp/ i\\Niii/
        iii/
        PATT:ppp$
        HOLD:$
        COMM:/zzz/ a\\Naaa
        PATT:ppp$
        HOLD:$
        ppp
        PATT:1$
        HOLD:$
        COMM:/ppp/ i\\Niii/
        PATT:1$
        HOLD:$
        COMM:/zzz/ a\\Naaa
        PATT:1$
        HOLD:$
        1
        PATT:2$
        HOLD:$
        COMM:/ppp/ i\\Niii/
        PATT:2$
        HOLD:$
        COMM:/zzz/ a\\Naaa
        PATT:2$
        HOLD:$
        2
        PATT:3$
        HOLD:$
        COMM:/ppp/ i\\Niii/
        PATT:3$
        HOLD:$
        COMM:/zzz/ a\\Naaa
        PATT:3$
        HOLD:$
        3
        PATT:zzz$
        HOLD:$
        COMM:/ppp/ i\\Niii/
        PATT:zzz$
        HOLD:$
        COMM:/zzz/ a\\Naaa
        PATT:zzz$
        HOLD:$
        zzz
        aaa
        PATT:1$
        HOLD:$
        COMM:/ppp/ i\\Niii/
        PATT:1$
        HOLD:$
        COMM:/zzz/ a\\Naaa
        PATT:1$
        HOLD:$
        1
        PATT:2$
        HOLD:$
        COMM:/ppp/ i\\Niii/
        PATT:2$
        HOLD:$
        COMM:/zzz/ a\\Naaa
        PATT:2$
        HOLD:$
        2
        PATT:3$
        HOLD:$
        COMM:/ppp/ i\\Niii/
        PATT:3$
        HOLD:$
        COMM:/zzz/ a\\Naaa
        PATT:3$
        HOLD:$
        3
        ```

2. 分析sed命令

    ```
    automation@watsng-ctrl-10-138-107-231:~$ sedsed -t -e ':1 /ppp/i iii' -e '/zzz/a aaa'
       linenr:1
        addr1:
    addr1flag:
        addr2:
    addr2flag:
     lastaddr:
     modifier:
           id::
      content:1
    delimiter:
      pattern:
      replace:
         flag:
      comment:

       linenr:1
        addr1:/ppp/
    addr1flag:
        addr2:
    addr2flag:
     lastaddr:
     modifier:
           id:i
      content:\@#linesep#@iii
    delimiter:
      pattern:
      replace:
         flag:
      comment:

       linenr:2
        addr1:/zzz/
    addr1flag:
        addr2:
    addr2flag:
     lastaddr:
     modifier:
           id:a
      content:\@#linesep#@aaa
    delimiter:
      pattern:
      replace:
         flag:
      comment:

    ```





99. 参考：
    - 官网：https://aurelio.net/projects/sedsed/
    - https://www.cnblogs.com/lemon-le/p/6061189.html