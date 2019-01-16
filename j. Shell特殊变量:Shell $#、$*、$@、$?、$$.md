上节我们讲到了 $n，它是特殊变量的一种，用来接收位置参数。本节我们继续讲解剩下的几个特殊变量，它们分别是：$#、$*、$@、$?、$$。

**Shell 特殊变量及其含义**

变量 | 含义 
:-----:|:------:
$0	    | 当前脚本的文件名。
$n（n≥1）| 传递给脚本或函数的参数。n 是一个数字，表示第几个参数。例如，第一个参数是 $1，第二个参数是 $2。
$#	|  传递给脚本或函数的参数个数。
$*	|  传递给脚本或函数的所有参数。
$@	|  传递给脚本或函数的所有参数。
$?	|  上个命令的退出状态，或函数的返回值。
$$	|  当前 Shell 进程 ID。对于 Shell 脚本，就是这些脚本所在的进程 ID。

下面我们通过两个例子来演示。

## 1) 给脚本文件传递参数

编写下面的代码，并保存为 test.sh：
```
#!/bin/bash
echo "Process ID: $$"
echo "File Name: $0"
echo "First Parameter : $1"
echo "Second Parameter : $2"
echo "All parameters 1: $@"
echo "All parameters 2: $*"
echo "Total: $#"
```
运行 test.sh，并附带参数：
```
$ chmod +x ./a.sh
$ ./test.sh Shell Linux
```
运行结果为：\
Process ID: 2788\
File Name: ./test.sh\
First Parameter : Shell\
Second Parameter : Linux\
All parameters 1: Shell Linux\
All parameters 2: Shell Linux\
Total: 2

## 2) 给函数传递参数

编写下面的代码，并保存为 test.sh：

```
#!/bin/bash
#定义函数
function func(){
    echo "Language: $1"
    echo "URL: $2"
    echo "First Parameter : $1"
    echo "Second Parameter : $2"
    echo "All parameters 1: $@"
    echo "All parameters 2: $*"
    echo "Total: $#"
}
#调用函数
func Java http://c.biancheng.net/java/
```
运行结果为：\
Language: Java\
URL: http://c.biancheng.net/java/\
First Parameter : Java\
Second Parameter : http://c.biancheng.net/java/\
All parameters 1: Java http://c.biancheng.net/java/\
All parameters 2: Java http://c.biancheng.net/java/\
Total: 2