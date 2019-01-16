在脚本语言中，字符串的拼接（也称字符串连接或者字符串合并）往往都非常简单，例如：
- 在 PHP 中，使用`.`即可连接两个字符串；
- 在 JavaScript 中，使用`+`即可将两个字符串合并为一个。

然而，在 Shell 中你不需要使用任何运算符，将两个字符串并排放在一起就能实现拼接，非常简单粗暴。请看下面的例子：
```
#!/bin/bash

name="Shell"
url="http://c.biancheng.net/shell/"
str1=$name$url  #中间不能有空格
str2="$name $url"  #如果被双引号包围，那么中间可以有空格
str3=$name": "$url  #中间可以出现别的字s符串
str4="$name: $url"  #这样写也可以
str5="${name}Script: ${url}index.html"  #这个时候需要给变量名加上大括号
echo $str1
echo $str2
echo $str3
echo $str4
echo $str5
```
运行结果：\
Shellhttp://c.biancheng.net/shell/ \
Shell http://c.biancheng.net/shell/ \
Shell: http://c.biancheng.net/shell/ \
Shell: http://c.biancheng.net/shell/ \
ShellScript: http://c.biancheng.net/shell/index.html

对于第 7 行代码，$name 和 $url 之间之所以不能出现空格，是因为当字符串不被任何一种引号包围时，遇到空格就认为字符串结束了，空格后边的内容会作为其他变量或者字符串解析，这一点在《Shell字符串》中已经提到。

对于第 10 行代码，加`{ }`是为了帮助解释器识别变量的边界，这一点在《Shell变量》中已经提到。