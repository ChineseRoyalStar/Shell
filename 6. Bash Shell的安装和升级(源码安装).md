一般而言，Bash Shell 是很多 Linux 发行版的默认 Shell，所以会随着系统的安装而自动安装。不过确实有一部分读者想要安装较新版本的 Bash Shell，所以本节会具体讲一下其安装方法，希望可以作为读者全新安装 Bash Shell 或者虽然已经安装但希望升级的参考。
## 确定你的 Shell 版本
如果你安装的 Linux 是 RedHat、CentOS、Fedora、Ubuntu、Debian 等主流发行版，那么在你的系统中很可能已经预装了 Bash Shell，只需要确认一下是否确实已经安装以及预装的版本即可。具体的方法是：
```
# 确认系统中使用的 Shell 是 bash
$ echo $SHELL
/bin/bash

# 查看系统中 Bash Shell 的版本（方法一）
$ bash --version
GNU bash, version 3.2.25(1)-release (i686-redhat-linux-gnu)
Copyright (C) 2005 Free Software Foundation, Inc.

# 查看系统中 Bash Shell 的版本（方法二）
$ echo $BASH_VERSION
3.2.25(1)-release
```
## 源码方式安装 Bash
Linux 下安装软件的方式无非是 RPM 包安装、yum 安装、源码安装三种方式，读者可以任选一种方式。

不过，相对来说 RPM 包安装和 yum 安装方式比较简单，若再考虑各种包的依赖关系，这两种方式中又属 yum 安装更为简单。这里就不详细介绍这两种安装方法了，下面会具体示范使用源码安装 bash 的过程。

首先访问 http://www.gnu.org/software/bash/bash.html 页面，在 Downloads 中选择一个下载的链接，笔者选择了中国科技大学提供的FTP下载目录：ftp://mirrors.ustc.edu.cn/gnu/bash/。

当前很多生产环境的系统中使用的 bash 版本还是 3.2 版，读者可以根据实际需要选择具体的版本。在笔者撰写本教程时，最新的版本是 4.2 版本，所以这里使用这个版本来做示范。

**1) 使用wget下载最新的 bash 源码包**

具体操作如下所示：
```
$ wget ftp://mirrors.ustc.edu.cn/gnu/bash/bash-4.2.tar.gz
--2013-04-11 19:37:41--  ftp://mirrors.ustc.edu.cn/gnu/bash/bash-4.2.tar.gz
           => &#x60;bash-4.2.tar.gz'
Resolving mirrors.ustc.edu.cn... 202.141.160.110, 2001:da8:d800:95::110
Connecting to mirrors.ustc.edu.cn|202.141.160.110|:21... connected.
Logging in as anonymous ... Logged in!
==> SYST ... done.    ==> PWD ... done.
==> TYPE I ... done.  ==> CWD /gnu/bash ... done.
==> SIZE bash-4.2.tar.gz ... 7009201
==> PASV ... done.    ==> RETR bash-4.2.tar.gz ... done.
Length: 7009201 (6.7M)
100%[==========================================>] 7,009,201   1.93M/s   in 3.5s  
2013-04-11 19:37:46 (1.89 MB/s) - &#x60;bash-4.2.tar.gz' saved [7009201]
```

**2) 解压源码包**

解压源码包并进入生成的目录中：
```
# 解压后会在当前目录下生成一个bash-4.2目录
$ tar zxvf bash-4.2.tar.gz

#进入目录bash-4.2
$ cd bash-4.2
$
```

**3) 准备配置（configure）**

最简单的配置方式是直接运行当前目录下的 configure，这会将 bash 安装到 /usr/local 目录中，不过编译安装软件时，好的习惯是使用--prefix参数指定安装目录。所以这里采用下面的配置方式。该条命令将会产生大量的输出，一开始会检查系统的编译环境以及相关的依赖软件。

最常见的错误可能是系统中没有安装 gcc 造成无法继续，如果是这个原因，使用 yum install gcc 命令进行安装。如果配置过程出现致命错误会立即退出，请读者注意输出内容中的 error 部分。
```
$ ./configure --prefix=/usr/local/bash4.2
checking build system type... i686-pc-linux-gnu
checking host system type... i686-pc-linux-gnu
Beginning configuration for bash-4.2-release for i686-pc-linux-gnu
checking for gcc... gcc
checking for C compiler default output file name... a.out
checking whether the C compiler works... Yes
......(略去内容)......

#如果大量的 checking 没问题，则配置环境检测通过。如果读者看到如下的输出内容，说明配置成功
configure: creating ./config.status
config.status: creating Makefile
config.status: creating builtins/Makefile
config.status: creating lib/readline/Makefile
config.status: creating lib/glob/Makefile
config.status: creating lib/intl/Makefile
config.status: creating lib/malloc/Makefile
config.status: creating lib/sh/Makefile
config.status: creating lib/termcap/Makefile
config.status: creating lib/tilde/Makefile
config.status: creating doc/Makefile
config.status: creating support/Makefile
config.status: creating po/Makefile.in
config.status: creating examples/loadables/Makefile
config.status: creating examples/loadables/perl/Makefile
config.status: creating config.h
config.status: executing default-1 commands
config.status: creating po/POTFILES
config.status: creating po/Makefile
config.status: executing default commands

#如果配置成功，会在当前目录中生成Makefile
$ ll Makefile
-rw-r--r-- 1 root root 77119 Apr 11 19:49 Makefile
```

**4) 正式编译**

```
#编译过程会产生大量输出
$ make
rm -f mksyntax
gcc  -DPROGRAM='"bash"' -DCONF_HOSTTYPE='"i686"'
-DCONF_OSTYPE='"linux-gnu"' -DCONF_MACHTYPE='"i686-pc-linux-gnu"'
-DCONF_VENDOR='"pc"'
-DLOCALEDIR='"/usr/local/bash4.2/share/locale"'
-DPACKAGE='"bash"' -DSHELL -DHAVE_CONFIG_H   -I.  -I. -I./include
-I./lib   -g  -o mksyntax ./mksyntax.c
......(略去内容)......
```

**5) 安装**

有时在安装前也可以进行测试，但是一般情况下这不是必需的。
```
#非必要步骤：测试安装
#[root@localhost bash-4.2]# make test
#安装
$ make install

#安装其实就是将make产生的文件复制到指定的目录中，在这里指定的目录就是之前我们用 --prefix 参数指定的/usr/local，可以在该目录中发现bash4.2目录
$ ls -ld /usr/local/bash4.2/
drwxr-xr-x 4 root root 4096 Apr 11 20:08 /usr/local/bash4.2/
```
到此为止，最新版本的 bash 就已经安装好了，确切地说是安装到了 /usr/local/bash4.2 中。

## 使用新版本的 Bash Shell

虽然最新版的 bash 已经安装到系统中，但是还需要经过一些设置才能使用。首先需要将最新的 bash 的路径写到 /etc/shells 中，以向系统注册新 Shell 的路径。可以采取直接编辑 /etc/shells 文件的方式，或者采用如下更简单的方式：
```
$ echo "/usr/local/bash4.2/bin/bash" >> /etc/shells

然后使用命令 chsh（change shell 的简写）修改登录 Shell。
$ chsh
Changing shell for root.
New shell [/bin/bash]: /usr/local/bash4.2/bin/bash #输入要修改的shell
Shell changed. #显示成功修改了shell

#此处chsh并没有附加参数，所以默认是修改root的shell，如要改变其他用户的登录shell，可以在后面跟上用户名，使用这种方式给用户john更改shell
$ chsh john
```
chsh 命令做的工作就是修改了 /etc/passwd 文件中登录 Shell 的路径，所以如果明白了 chsh 的原理，实际上可以手工编辑 /etc/passwd 文件，将 root 用户的这行改成下面的样子（这又一次印证了 Linux 中一切皆文件的说法）：
```
$ cat /etc/passwd | grep bash4.2
root:x:0:0:root:/root:/usr/local/bash4.2/bin/bash
```
最后还需要重新登录以获得 Shell，登录后再次验证一下当前的 Shell 版本。