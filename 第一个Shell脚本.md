## 第一个Shell脚本

几乎所有编程语言的教程都是从使用著名的“Hello World”开始的，出于对这种传统的尊重（或者说落入俗套），我们的第一个 Shell 脚本也输出“Hello World”。
s
打开文本编辑器，新建一个文本文件，并命名为 test.sh。
```
扩展名sh代表 shell，扩展名并不影响脚本执行，见名知意就好，如果你用 php 写 shell 脚本，扩展名就用php好了。
```
在 test.sh 中输入代码：
```
#!/bin/bash
echo "Hello World !"  #这是一条语句
```
第 1 行的`#!`是一个约定的标记，它告诉系统这个脚本需要什么解释器来执行，即使用哪一种Shell；后面的`/bin/bash`就是指明了解释器的具体位置。

第 2 行的 `echo` 命令用于向标准输出文件（**Standard Output**，stdout，一般就是指终端）输出文本。在`.sh`文件中使用命令与在终端直接输入命令的效果是一样的。

第 2 行的`#`及其后面的内容是注释。Shell 脚本中所有以`#`开头的都是注释（当然以`#!`开头的除外）。写脚本的时候，多写注释是非常有必要的，以方便其他人能看懂你的脚本，也方便后期自己维护时看懂自己的脚本——实际上，即便是自己写的脚本，在经过一段时间后也很容易忘记。

下面给出了一段稍微复杂的 Shell 脚本：
```
#!/bin/bash
# Copyright (c) http://c.biancheng.net/shell/ss

echo "What is your name?"
read PERSON
echo "Hello, $PERSON"
```
第 5 行中表示从终端读取用户输入的数据，并赋值给 PERSON 变量。read 命令用来从标准输入文件（**Standard Input**，stdin，一般就是指终端）读取用户输入的数据。

第 6 行表示输出变量 PERSON 的内容。注意在变量名前边要加上`$`，否则变量名会作为字符串的一部分处理。