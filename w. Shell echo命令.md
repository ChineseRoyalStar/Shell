echo 是一个 Shell 内建命令，用来在终端输出字符串，并在最后默认加上换行符。请看下面的例子：
```
#!/bin/bash

name="Shell教程"
url="http://c.biancheng.net/shell/"

echo "读者，你好！"  #直接输出字符串
echo $url  #输出变量
echo "${name}的网址是：${url}"  #双引号包围的字符串中可以解析变量
echo '${name}的网址是：${url}'  #单引号包围的字符串中不能解析变量
```
运行结果：
```
读者，你好！  
http://c.biancheng.net/shell/  
Shell教程的网址是：http://c.biancheng.net/shell/  
${name}的网址是：${url} 
```

## 不换行

echo 命令输出结束后默认会换行，如果不希望换行，可以加上-n参数，如下所示：
```
#!/bin/bash

name="Tom"
age=20
height=175
weight=62

echo -n "${name} is ${age} years old, "
echo -n "${height}cm in height "
echo "and ${weight}kg in weight."
echo "Thank you!"
```
运行结果：
```
Tom is 20 years old, 175cm in height and 62kg in weight.
Thank you!
```

## 输出转义字符

默认情况下，echo 不会解析以反斜杠`\`开头的转义字符。比如，`\n`表示换行，echo 默认会将它作为普通字符对待。请看下面的例子：
```
[root@localhost ~]# echo "hello \nworld"
hello \nworld
```
我们可以添加`-e`参数来让 echo 命令解析转义字符。例如：
```
[root@localhost ~]# echo -e "hello \nworld"
hello
world
```
##### \c 转义字符

有了`-e`参数，我们也可以使用转义字符`\c`来强制 echo 命令不换行了。请看下面的例子：
```
#!/bin/bash

name="Tom"
age=20
height=175
weight=62

echo -e "${name} is ${age} years old, \c"
echo -e "${height}cm in height \c"
echo "and ${weight}kg in weight."
echo "Thank you!"
```
运行结果：
```
Tom is 20 years old, 175cm in height and 62kg in weight.
Thank you!
```