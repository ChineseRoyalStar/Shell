## 作为可执行程序

Shell 脚本也是一种解释执行的程序，可以在终端直接调用（需要使用 chmod 命令给 Shell 脚本加上执行权限），如下所示：
```
$ cd demo  #切换到 test.sh 所在的目录
$ chmod +x ./test.sh  #使脚本具有执行权限
$ ./test.sh  #执行脚本
```
第 2 行中，chmod +x表示给 test.sh 增加执行权限。

第 3 行中，`./`表示当前目录，整条命令的意思是执行当前目录下的 test.sh 脚本。如果不写`./`，Linux 会到系统路径（由 PATH 环境变量指定）下查找 test.sh，而系统路径下显然不存在这个脚本，所以会执行失败。

通过这种方式运行脚本，第一行一定要写对，好让系统查找到正确的解释器。

**1) 使用点号“.”**

点号用于执行某个脚本，甚至脚本没有可执行权限也可以运行。有时候在测试运行某个脚本时可能并不想为此修改脚本权限，这时候就可以使用.来运行脚本，非常方便。

编写下面的代码并保存为 test.sh:
```
#!/bin/bash
echo "http://c.biancheng.net/shell/"
```
如果没有运行权限的话，用`./`执行就会有报错，但是若在其前面使用点号来执行就不会报错，如下所示：
```
$ ./test.sh
bash: .test.sh: Permission denied
```
使用.增加 test.sh 的执行权限，就可以正常运行了：
```
$ . ./test.sh
http://c.biancheng.net/shell/
```
**2) 使用 source 命令**

与点号类似，source 命令也可读取并在当前环境中执行脚本，同时还可返回脚本中最后一个命令的返回状态；如果没有返回值则返回 0，代表执行成功；如果未找到指定的脚本则返回 false。
```
$ source test.sh
http://c.biancheng.net/shell/
```
## 作为解释器参数

这种运行方式是，直接运行解释器，其参数就是 shell 脚本的文件名，如：
```
$ /bin/bash test.sh
http://c.biancheng.net/shell/
```
这种方式运行的脚本，不需要在第一行指定解释器信息，写了也没用。
```
#!/bin/bash
# Copyright (c) http://c.biancheng.net/shell/

echo "What is your name?"
read PERSON
echo "Hello, $PERSON"
```
运行脚本：
```
$ chmod +x ./test.sh
$ ./test.sh
What is your name?
mozhiyan
Hello, mozhiyan
$
```