所谓 Shell 内建命令，就是由 Bash 自身提供的命令，而不是文件系统中的某个可执行文件。

例如，用于进入或者切换目录的 cd 命令，虽然我们一直在使用它，但如果不加以注意很难意识到它与普通命令的性质是不一样的：该命令并不是某个外部文件，只要在 Shell 中你就一定可以运行这个命令。

可以使用 type 来确定一个命令是否是内建命令：
```
[root@localhost ~]# type cd
cd is a Shell builtin
[root@localhost ~]# type ifconfig
ifconfig is /sbin/ifconfig
```
由此可见，cd 是一个 Shell 内建命令，而 ifconfig 是一个外部文件，它的位置是`/sbin/ifconfig`。

还记得系统变量 $PATH 吗？$PATH 变量包含的目录中几乎聚集了系统中绝大多数的可执行命令，它们都是外部命令。

通常来说，内建命令会比外部命令执行得更快，执行外部命令时不但会触发磁盘 I/O，还需要 fork 出一个单独的进程来执行，执行完成后再退出。而执行内建命令相当于调用当前 Shell 进程的一个函数。

Shell 的内建命令众多，在 3.2.25 版本的 Bash 中有几十个，如下所示：

| | | | | | |
--|---|---|---|---|---|
bash	|$:	.	|[	|alias	|bg	|bind
break	|builtin|cd	|command |compgen |complete |continue
declare	|dirs	|disown	|echo	|enable	|eval	|exec
exit	|export	|fc	|fg	|getopts	|hash	|help
history	|jobs	|kill	|let	|local	|logout	|popd
printf	|pushd	|pwd	|read	|readonly	|return	|set
shift	|shopt	|source	|suspend	|test	|times	|trap
type	|typeset	|ulimit	|umask	|unalias	|unset	|wait