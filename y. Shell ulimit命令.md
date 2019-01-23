系统的可用资源是有限的，如果不限制用户和进程对系统资源的使用，则很容易陷入资源耗尽的地步，而使用 ulimit 命令可以控制进程对可用资源的访问（ulimit 是一个 Shell 内置命令）。

默认情况下 Linux 系统的各个资源都做了软硬限制，其中硬限制的作用是控制软限制（换言之，软限制不能高于硬限制）。使用ulimit -a可以查看当前系统的软限制，使用命令`ulimit -a –H`可查看系统的硬限制。

下面是该命令的运行结果，笔者对每行输出都做了注解。
```
[root@localhost ~]# ulimit -a
#core文件大小，单位是block，默认为0
core file size          (blocks, -c) 0
#数据段大小，单位是kbyte，默认不做限制
data seg size           (kbytes, -d) unlimited
#调度优先级，默认为0
scheduling priority             (-e) 0
#创建文件的大小，单位是block，默认不做限制
file size               (blocks, -f) unlimited
#挂起的信号数量，默认是8192
pending signals                 (-i) 8192
#最大锁定内存的值，单位是kbyte，默认是32
max locked memory       (kbytes, -l) 32
#最大可用的常驻内存值，单位是kbyte，默认不做限制
max memory size         (kbytes, -m) unlimited
#最大打开的文件数，默认是1024
open files                      (-n) 1024
#管道最大缓冲区的值
pipe size            (512 bytes, -p) 8
#消息队列的最大值，单位是byte
POSIX message queues     (bytes, -q) 819200
#程序的实时性优先级，默认为0
real-time priority              (-r) 0
#栈大小，单位是kbyte
stack size              (kbytes, -s) 10240
#最大cpu占用时间，默认不做限制
cpu time               (seconds, -t) unlimited
#用户最大进程数，默认是8192
max user processes              (-u) 8192
#最大虚拟内存，单位是kbyte，默认不做限制
virtual memory          (kbytes, -v) unlimited
#文件锁，默认不做限制
file locks                      (-x) unlimited
```
每一行中都包含了相应的改变该项设置的参数，以最大可以打开的文件数为例（open files 默认是 1024），想要增大至 4096 则按照如下命令设置（可参照此方法调整其他参数）。
```
#设置最大打开的文件数
#该命令会同时设置硬限制和软限制
[root@localhost ~]# ulimit -n 4096
#使用-S参数单独设置软限制
#[root@localhost ~]# ulimit -S -n 4096
#使用-H参数单独设置硬限制
#[root@localhost ~]# ulimit -H -n 4096
```
使用 ulimit 直接调整参数，只会在当前运行时生效，一旦系统重启，所有调整过的参数就会变回系统默认值。所以建议将所有的改动放在 ulimit 的系统配置文件中。相关配置方法请参考笔者对相关配置文件的注释。
```
[root@localhost ~]# cat /etc/security/limits.conf
# /etc/security/limits.conf
#该文件是ulimit的配置文件，任何对系统的ulimit的修改都应该写入该文件
#请将所有的设置写到该文件的最后
#Each line describes a limit for a user in the form:
#配置应该写成下面这行的格式，即每个配置占用1行，每行4列
#每列分别是<domain> <type> <item> <value>
#<domain>        <type>  <item>  <value>
#
#其中：
#<domain>可以取的值如下：
#       - 一个用户名
#       - 一个组名，组名前面用@符号
#       - 通配符*
#       - 通配符%
#Where:
#<domain> can be:
#        - an user name
#        - a group name, with @group syntax
#        - the wildcard *, for default entry
#        - the wildcard %, can be also used with %group syntax,
#                 for maxlogin limit
#
#<type>只有以下两个可用值：
#       - soft用于设置软限制
#       - hard用于设置硬限制
#<type> can have the two values:
#        - "soft" for enforcing the soft limits
#        - "hard" for enforcing hard limits
#
#<item>的值可以是以下任意一种：
#        - core - core文件大小的限制 (KB)
#        - data - 最大数据段限制 (KB)
#        - fsize - 最大文件大小 (KB)
#        - memlock - 最大锁定的内存大小 (KB)
#        - nofile - 最大打开文件数
#        - rss - 最大常驻内存值 (KB)
#        - stack - 最大栈空间大小 (KB)
#        - cpu - 最大CPU使用时间 (MIN)
#        - nproc - 最大进程数
#        - as - 虚拟地址空间
#        - maxlogins - 某用户的最大登录数
#        - maxsyslogins - 系统用户最大登录数
#        - priority - 用户进程的运行优先级
#        - locks – 用户最大可以锁定文件的数量
#        - sigpending - 最大挂起的信号量数
#        - msgqueue - POSIX信号队列使用的最大内存值 (bytes)
#        - nice - 最大nice值
#        - rtprio - 最大实时优先级
#
#<item> can be one of the following:
#        - core - limits the core file size (KB)
#        - data - max data size (KB)
#        - fsize - maximum filesize (KB)
#        - memlock - max locked-in-memory address space (KB)
#        - nofile - max number of open files
#        - rss - max resident set size (KB)
#        - stack - max stack size (KB)
#        - cpu - max CPU time (MIN)
#        - nproc - max number of processes
#        - as - address space limit
#        - maxlogins - max number of logins for this user
#        - maxsyslogins - max number of logins on the system
#        - priority - the priority to run user process with
#        - locks - max number of file locks the user can hold
#        - sigpending - max number of pending signals
#        - msgqueue - max memory used by POSIX message queues (bytes)
#        - nice - max nice priority allowed to raise to
#        - rtprio - max realtime priority
#
#<domain>      <type>  <item>         <value>
#
#以下是使用样例，请参照配置
#*               soft    core            0
#*               hard    rss             10000
#@student        hard    nproc           20
#@faculty        soft    nproc           20
#@faculty        hard    nproc           50
#ftp             hard    nproc           0
#@student        -       maxlogins       4
```