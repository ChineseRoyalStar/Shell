exit 是一个 Shell 内置命令，用来退出当前 Shell：
- 如果在终端中直接运行 exit 命令，会退出当前登录的 Shell，并关闭终端；
- 如果在 Shell 脚本中出现 exit 命令，会停止执行后边的所有代码，立即退出 Shell 脚本。

exit 命令可以接受的参数是一个状态值 n，代表退出时的状态。如果不指定，默认状态值是 0。

以下面的 Shell 脚本（命名为 demo.sh）为例：
```
#!/bin/bash

echo "befor exit"
exit 8
echo "after exit"
```
运行该脚本：
```
[root@localhost ~]# bash ./demo.sh
befor exit
```
可以看到，`"after exit"`并没有输出，这说明遇到 exit 命令后，demo.sh 执行就结束了。

>注意，必须将 Shell 脚本作为解释器参数来运行，不能将 Shell 脚本作为可执行程序运行。这两种运行方式我们已在《执行Shell脚本》中讲到

我们可以紧接着使用 $? 来获取 demo.sh 的退出状态：
```
[root@localhost ~]# echo $?
8
```