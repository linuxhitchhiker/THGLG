---
title: "编写简单的 Shell 脚本"
comments: true
---

# 编写简单的 Shell 脚本

Shell 脚本（Shell Script) 脚本提供了一个非常便捷地完成许多图形化界面无法完成的任务的方式。它本质是由许多命令和逻辑语法组合而成，后缀通常为 `.sh` 的纯文本文件。你可以使用任意的文本编辑器打开 shell 脚本，并编辑或保存内容。

以下是一个简单的 shell 脚本样例：

```shell
bh@c004-h0:~> cat example.sh
#!/bin/sh
#  打印下列行：
echo "Hello World!"
```

所有的脚本都以 `#!` 符号（[Shebang](https://zh.wikipedia.org/wiki/Shebang)）开头，表明这是一个 shell 脚本。而紧随其后的 `/bin/sh` 则是脚本指定的解释器。

第二行是注释，shell 在执行脚本时，会自动忽略所有以 `#` 符号开头的行。注释有助于帮助阅读者快速了解这个脚本的功能或者其他内容。

第三方则是命令，`echo` 会将 `Hello World` 打印在终端输出之中。

在运行脚本之前，你需要完成以下几件事：

1. 每个脚本必须包含 Shebang 符号，如果你没有输入该行，则需要手动指定运行脚本的程序。
2. 你可以将脚本保存到任意位置，但为了使用方便，建议将脚本存放到你的 `$PATH` 变量包含的文件夹中，这样当你登陆 shell 会话时，shell 就能直接检索到你需要使用的脚本。
3. 为脚本赋予可执行权限，否则你需要 `sudo` 权限才能运行脚本：  
    ```
    $ chmod +x ~/exmaple.sh #为该脚本添加可执行权限
    ```

要执行脚本，你可以使用相对或绝对路径来执行脚本。在本例中，如下：

```
bh@c004-h0:~> ./example.sh
Hello World!
bh@c004-h0:~> cd /; ./home/bh/example.sh
Hello World!
```

如果你将文件存放到 `$PATH` 变量包含的文件夹中，你只需要输入文件名即可运行脚本：

```
bh@c004-h0:~> echo $PATH
/home/bh/.local/bin:/usr/local/bin:/usr/bin:/bin
bh@c004-h0:~> mv example.sh ~/.local/bin
bh@c004-h0:~> example.sh
Hello World!
```

## 扩展你的脚本

在 shell 脚本中，你可以使用你在终端中能够使用的一切命令，元符号或各种组合方法等前文提到的有关于终端的知识。

### 使用简单的流结构

#### if 命令

你可以使用 `while`、`if`、`for` 和 `case` 控制你的脚本的流结构（flow constructs）。

`if` 命令用于检查表达式，如下：

```shell
#!/bin/sh
if test $USER = "bh" ; then 
#检查条件，检查当前用户是否是 `bh`
    echo "Hello bh."
    #如果是则打印上述内容
else
#表示或者，or
    echo "You are not bh."
    #如果不符合条件，则打印上述内容
fi
#脚本在此结束
```

表达式可以复杂或简单，更多内容详见[此处](https://bash.cyberciti.biz/guide/If..else..fi)。

#### for 命令

for 循环允许你对条目列表执行命令。例如，下面的代码打印了当前目录中 PNG 文件的一些信息：

```shell
#!/bin/sh
for i in *.png; do
    ls -l $i
done
```

## 更多信息

你可以使用 `$ man bash` 命令查询更多的帮助或文档信息。或者点击下列链接深入阅读香港的内容。

- [Bash Guide for Beginners](http://tldp.org/LDP/Bash-Beginners-Guide/html/index.html)
- [BASH Programming - Introduction HOW-TO](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html)
- [Advanced Bash-Scripting Guide](http://tldp.org/LDP/abs/html/index.html)
- [Sh - the Bourne Shell](http://www.grymoire.com/Unix/Sh.html)