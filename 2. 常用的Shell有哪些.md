## 常用的Shell有哪些

Linux 是一个开源的操作系统，由分布在世界各地的多个组织机构或个人共同开发完成，每个组织结构或个人负责一部分功能，最后组合在一起，就构成了今天的 Linux。例如：
- Linux 内核最初由芬兰黑客 Linus Torvalds 开发，后来他组建了团队,Linux 内核由这个团队维护。
- GNU 组织开发了很多核心软件和基础库，例如 GCC 编译器、C语言标准库、文本编辑器 Emacs、进程管理软件、Shell 以及 GNOME 桌面环境等。
- VIM 编辑器由荷兰人 Bram Moolenaar 开发。

Windows、Mac OS、Android 等操作系统不一样，它们都由一家公司开发，所有的核心软件和基础库都由一家公司做决定，容易形成统一的标准，一般不会开发多款功能类似的软件。

而 Linux 不一样，它是“万国牌”，由多个组织机构开发，不同的组织机构为了发展自己的 Linux 分支可能会开发出功能类似的软件，它们各有优缺点，用户可以自由选择。Shell 就是这样的一款软件，不同的组织机构开发了不同的 Shell，它们各有所长，有的占用资源少，有的支持高级编程功能，有的兼容性好，有的重视用户体验。
>Shell 既是一种脚本编程语言，也是一个连接内核和用户的软件。
常见的 Shell 有**sh、bash、csh、tcsh、ash**等。

### sh

sh 的全称是 Bourne shell，由 AT&T 公司的 Steve Bourne开发，为了纪念他，就用他的名字命名了。

sh 是 UNIX 上的标准 shell，很多 UNIX 版本都配有 sh。sh 是第一个流行的 Shell。

### csh

sh 之后另一个广为流传的 shell 是由柏克莱大学的 Bill Joy 设计的，这个 shell 的语法有点类似C语言，所以才得名为 C shell ，简称为 csh。

Bill Joy 是一个风云人物，他创立了 BSD 操作系统，开发了 vi 编辑器，还是 Sun 公司的创始人之一。

>BSD 是 UNIX 的一个重要分支，后人在此基础上发展出了很多现代的操作系统，最著名的有 FreeBSD、OpenBSD 和 NetBSD，就连 Mac OS X 在很大程度上也基于BSD。

### tcsh

tcsh 是 csh 的增强版，加入了命令补全功能，提供了更加强大的语法支持。

### ash

一个简单的轻量级的 Shell，占用资源少，适合运行于低内存环境，但是与下面讲到的 bash shell 完全兼容。

### bash

bash shell 是 Linux 的默认 shell，本教程也基于 bash 编写。

bash 由 GNU 组织开发，保持了对 sh shell 的兼容性，是各种 Linux 发行版默认配置的 shell。
>bash 兼容 sh 意味着，针对 sh 编写的 Shell 代码可以不加修改地在 bash 中运行。
尽管如此，bash 和 sh 还是有一些不同之处：
- 一方面，bash 扩展了一些命令和参数；
- 另一方面，bash 并不完全和 sh 兼容，它们有些行为并不一致，但在大多数企业运维的情况下区别不大，特殊场景可以使用 bash 代替 sh。

## 查看 Shell
Shell 是一个程序，一般都是放在/bin或者/user/bin目录下，当前 Linux 系统可用的 Shell 都记录在/etc/shells文件中。/etc/shells是一个纯文本文件，你可以在图形界面下打开它，也可以使用 cat 命令查看它。

通过 cat 命令来查看当前 Linux 系统的可用 Shell：
```
$ cat /etc/shells
/bin/sh
/bin/bash
/sbin/nologin
/usr/bin/sh
/usr/bin/bash
/usr/sbin/nologin
/bin/tcsh
/bin/csh
```

在现代的 Linux 上，sh 已经被 bash 代替，`/bin/sh`往往是指向`/bin/bash`的符号链接。

如果你希望查看当前 Linux 的默认 Shell，那么可以输出 SHELL 环境变量：
```
$ echo $SHELL
/bin/bash
```
**输出结果表明默认的 Shell 是 bash。**

`echo`是一个 Shell 命令，用来输出变量的值，我们将在《Shell echo命令》中详细介绍它的用法。SHELL是 Linux 系统中的环境变量，它指明了当前使用的 Shell 程序的位置，也就是使用的哪个 Shell。
