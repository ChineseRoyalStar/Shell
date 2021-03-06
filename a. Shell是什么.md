# shell是什么？1分钟理解shell的概念！

现在我们使用的操作系统（Windows、Mac OS、Android、iOS 等）都是带图形界面的，简单直观，容易上手，对专业用户（程序员、网管等）和普通用户（家庭主妇、老年人等）都非常适用；计算机的普及离不开图形界面。

然而在计算机的早期并没有图形界面，我们只能通过一个一个地命令来控制计算机，这些命令有成百上千之多，且不说记住这些命令非常困难，每天面对没有任何色彩的“黑屏”本身就是一件枯燥的事情；这个时候的计算机还远远谈不上炫酷和普及，只有专业人员才能使用。

对于图形界面，用户点击某个图标就能启动某个程序；对于命令行，用户输入某个程序的名字（可以看做一个命令）就能启动某个程序。这两者的基本过程都是类似的，都需要查找程序在硬盘上的安装位置，然后将它们加载到内存运行。

**换句话说，图形界面和命令行要达到的目的是一样的，都是让用户控制计算机。**

然而，真正能够控制计算机硬件（CPU、内存、显示器等）的只有操作系统内核（Kernel），图形界面和命令行只是架设在用户和内核之间的一座桥梁。

由于安全、复杂、繁琐等原因，用户不能直接接触内核（也没有必要），需要另外再开发一个程序，让用户直接使用这个程序；该程序的作用就是接收用户的操作（点击图标、输入命令），并进行简单的处理，然后再传递给内核。如此一来，用户和内核之间就多了一层“代理”，这层“代理”既简化了用户的操作，也保护了内核。

**用户界面和命令行就是这个另外开发的程序，就是这层“代理”。在Linux下，这个命令行程序叫做 Shell。**

Shell 除了能解释用户输入的命令，将它传递给内核，还可以：
- 用其他程序，给其他程序传递数据或参数，并获取程序的处理结果；
- 在多个程序之间传递数据，把一个程序的输出作为另一个程序的输入；
- Shell 本身也可以被其他程序调用。

由此可见，Shell 是将内核、程序和用户连接了起来。

Shell 本身支持的命令并不多，但是它可以调用其他的程序，每个程序就是一个命令，这使得 Shell 命令的数量可以无限扩展，其结果就是 Shell 的功能非常强大，完全能够胜任 Linux 的日常管理工作，如文本或字符串检索、文件的查找或创建、大规模软件的自动部署、更改系统设置、监控服务器性能、发送报警邮件、抓取网页内容、压缩文件等。

Shell 并不是简单的堆砌命令，我们还可以在 Shell 中编程，这和使用 C/C++、Java、Python 等常见的编程语言并没有什么两样。

Shell 虽然没有 C/C++、Java、Python 等强大，但也支持了基本的编程元素，例如：
- if...else 选择结构，switch...case 开关语句，for、while、until 循环；
- 变量、数组、字符串、注释、加减乘除、逻辑运算等概念；
- 函数，包括用户自定义的函数和内置函数（例如 printf、export、eval 等）。

站在这个角度讲，Shell 也是一种编程语言，它的编译器（解释器）是 Shell 这个程序。我们平时所说的 Shell，有时候是指连接用户和内核的这个程序，有时候又是指 Shell 编程。

Shell 主要用来开发一些实用的、自动化的小工具，而不是用来开发具有复杂业务逻辑的中大型软件，例如检测计算机的硬件参数、一键搭建Web开发环境、日志分析等，Shell 都非常合适。

使用 Shell 的熟练程度反映了用户对 Linux 的掌握程度，运维工程师、网络管理员、程序员都应该学习 Shell。

尤其是 Linux 运维工程师，Shell 更是必不可少的，是必须掌握的技能，它使得我们能够自动化地管理服务器集群，否则你就得一个一个地登录所有的服务器，对每一台服务器都进行相同的设置，而这些服务器可能有成百上千之多，会浪费大量的时间在重复性的工作上。

# Shell 是一种脚本语言

任何代码最终都要被“翻译”成二进制的形式才能在计算机中执行。

有的编程语言，如 C/C++、Pascal、Go语言、汇编等，必须在程序运行之前将所有代码都翻译成二进制形式，也就是生成可执行文件，用户拿到的是最终生成的可执行文件，看不到源码。

这个过程叫做**编译（Compile）**，这样的编程语言叫做编译型语言，完成编译过程的软件叫做**编译器（Compiler）**。

而有的编程语言，如 Shell、JavaScript、Python、PHP等，需要一边执行一边翻译，不会生成任何可执行文件，用户必须拿到源码才能运行程序。程序运行后会即时翻译，翻译完一部分执行一部分，不用等到所有代码都翻译完。

这个过程叫做解释，这样的编程语言叫做<font color=#228B22>解释型语言**脚本语言（Script）**，完成解释过程的软件叫做**解释器**。

编译型语言的优点是执行速度快、对硬件要求低、保密性好，适合开发操作系统、大型应用程序、数据库等。

脚本语言的优点是使用灵活、部署容易、跨平台性好，非常适合Web开发以及小工具的制作。

Shell 就是一种脚本语言，我们编写完源码后不用编译，直接运行源码即可。