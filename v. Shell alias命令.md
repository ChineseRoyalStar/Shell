alias 用来给命令创建一个别名。若直接输入该命令且不带任何参数，则列出当前 Shell 环境中使用了哪些别名。现在你应该能理解类似`ll`这样的命令为什么与`ls -l`的效果是一样的吧。

>alisa 是一个 Shell 内建命令。

下面让我们来看一下有哪些命令被默认创建了别名:
```
[root@localhost ~]# alias
alias cp='cp -i'
alias l.='ls -d .* --color=tty'
alias ll='ls -l --color=tty'
alias ls='ls --color=tty'
alias mv='mv -i'
alias rm='rm -i'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
```
你看，为了让我们使用方便，Shell 会给某些命令默认创建别名。

使用 alias 当然也可以自定义别名，比如说一般的关机命令是`shutdown-h now`，写起来比较长，这时可以重新定义一个关机命令，以后就方便多了。使用 alias 定义的别名命令也是支持 Tab 键补全的，如下所示：
```
alias myShutdown='shutdown -h now'
```
注意，这样定义别名只能在当前 Shell 环境中有效，换句话说，重新登录后这个别名就消失了。为了确保永远生效，可以将该别名手动写入到用户主目录中的`.bashrc`文件。

>`.bashrc`其实也是一个 Shell 脚本文件，该文件专门用来存放用户自定义的别名和函数。

将别名写入.bashrc文件后的效果如下所示：
```
# .bashrc
# User specific aliases and functions
alias myShutdown='shutdown -h now'

# Source global definitions
if [ -f /etc/bashrc ]; then
    . /etc/bashrc
fi
```

## unalias：删除别名

使用 unalias 内建命令可以删除当前 Shell 环境中的别名。unalias 有两种使用方法：
- 第一种用法是在命令后跟上某个命令的别名，用于删除指定的别名。
- 第二种用法是在命令后接-a参数，删除当前 Shell 环境中所有的别名。

同样，这两种方法都是在当前 Shell 环境中生效的。要想永久删除在`.bashrc`文件中定义的别名，只能进入该文件手动删除。
```
# 删除 ll 别名
[root@e-bai ~]# unalias ll
# 再次运行该命令时，报“找不到该命令”的错误，说明该别名被删除了
[root@e-bai ~]# ll
-bash: ll: command not found
```