# 历史相关

**GNU**

GNU is Not Unix。由Stallman创建，GNU项目的目的是创建一个自由，免费的Unix操作系统。最终走了迂回路线，没有直接创造出免费的Unix，但是有众多运行在Unix上的产品。

* Emacs

* GNU C Compiler——gcc

* GNU C Library——glibc

* Bash Shell

**GPL**

GNU General Public License。GNU避免自由软件被拿去做成商业软件而拟的一份法律声明。体现自由软件的精神。



显示一下Hello World，看看系统是否正常
`echo 'Hello World'`{{execute}}

看看系统的
`uname -r`{{execute}}

`lsb_release -a`{{execute}}


# linux介绍

# 1. Linux的版本

_主版本.次版本.释出版本-修改版本_

次版本为奇数：development；为偶数：stable。

命令：

```shell

`uname -r #3.16.0-23-generic`{{execute}}

lsb_release -a #

//output

Distributor ID: Ubuntu

Description: Ubuntu 14.10

Release: 14.10

Codename: utopic

```

**Distribution**:Kernel + Softwares + Tools 称为linux发行版。

**POSIX** Portable Operating System Interface，可携式操作系统接口——规范内核和应用程序之间的接口。

**LSB** Linux Standard Base。

**FHS** File system Hierarchy Standard。

Linux包含内核和系统调用。

Linux是没有图形界面的，所谓的图形界面是一套软件。X Window服务器是运行在Linux内核上的一套服务器软件，实行了X协议，X Client包括KDE，GNOME。

# 2. 终端

**Terminal**：我们并不是直接与系统打交道，而是通过一个叫做 Shell 的中间程序来完成的。gnome-terminal，kconsole，xterm，rxvt，kvt，nxterm 和 eterm，xfce 。

**tty**：\[Ctrl\]+\[Alt\]+\[F1\]～\[F6\]，\[Ctrl\]+\[Alt\]+\[F7\]，对应\/dev\/tty 设备。

**Shell类型**：UNIX\/Linux 中比较流行的常见的 Shell 有 bash，zsh，ksh，csh。

**风格切换**

```

set -o #查看

set -o vi #设置风格为vi

set -o emacs #设置风格为emacs ，默认的做法。

```

**常用终端按键**：

| 按键 | 作用 |

| --- | --- |

| Tab | 补全命令，按两下可以提示可以补全的 |

| Ctr+c | 停止Shell运行 |

| Ctrl+d | 键盘输入结束或退出终端 |

| Ctrl+s | 暂定当前程序，暂停后按下任意键恢复运行 |

| Ctrl+z | 将当前程序放到后台运行，恢复到前台为命令fg |

| Ctrl+a | 将光标移至输入行头，相当于Home键 |

| Ctrl+e | 将光标移至输入行末，相当于End键 |

| Ctrl+k | 删除从光标所在位置到行末 |

| Shift+PgUp | 将终端显示向上滚动 |

| Shift+PgDn | 将终端显示向下滚动 |

**Shell通配符**：

| 字符 | 含义 |

| --- | --- |

| \* | 闭包 |

| ? | 匹配任意一个字符 |

| \[abc\] | 匹配其中一个字符 |

| \[!abc\] | 均不能匹配 |

| \[c1-c2\] | 区间匹配，其中任意字符 |

| {c1..c2} | 匹配全部字符 |

| {string1,string2,...} | 匹配其中一个字符串 |

# 3. Manul Pages

man [options] [section] <command_name>

>帮助格式：名字，概要，描述，选项，返回值，参阅，Bug，文件，版权，作者

- -a：显示所有匹配的结果

- -d：调试信息

- -k：搜索特定字符串

- -w：打印帮助页的位置，而不是显示其内容。

```shell

man 1 ls # ls在第一区段的帮助手册

man mkfifo#显示第一个帮助文件

man -wa mkfifo #显示所有帮助页列表

man 3 mkfifo #显示第三区段的帮助页

man -a mkfifo #一次显示第一区段和第三区段，使用q退出之后，可以用Ctr+c中断后续的显示。

```

区段列表：

| 区段 | 说明 |

| --- | --- |

| 1 | 一般命令 |

| 2 | 系统调用 |

| 3 | 库函数，包含C标准函数库 |

| 4 | 特殊文件和驱动设备 |

| 5 | 文件格式和约定 |

| 6 | 游戏和屏保 |

| 7 | 杂项 |

| 8 | 系统管理和守护进程 |

# 4. 命令和文件查找

**which**——locate a command

```

which [-a] command #a：PATH中所有的命令，which从当前用户的PATH路径搜索，不同用户可能得到不同结果。

which ifconfig #/sbin/ifconfig

which which #

```

**whereis**——locate the binary, source, and manual page files for a command

```

whereis [-bmsu] command #b：binary，m：manual，s：source源文件，u：除掉这三者

whereis ifconfig #/sbin/ifconfig /user/share…/ifconfig.8.gz，对于不同的用户，搜索结果应该是相同的，因为不是从PATH查找。

whereis -m passwd

```

**locate**——find files by name

```

locate [-ir] keyword #i：忽略大小写，r：正则表达式

locate passwd

```

**find**——search for files in a directory hierarchy

```

find [path] [option] [action]

find /etc/ -name interfaces

find /home/pzdn/Code -name *.c -exec chmod g+w {} \;

```

与时间相关的选项：

![](/assets/linuxfind.png)

* mtime n: n 为数字，表示为在n天之前的“一天之内”修改过的文件

* mtime +n: 列出在n天之前（不包含n天本身）被修改过的文件

* mtime -n: 列出在n天之内（包含n天本身）被修改过的文件

* newer file: file为一个已存在的文件，列出比file还要新的文件名

时间参数：

-ctime：创建时间

-mtime：修改时间

-atime：访问时间

```

find ~ -mtime 0 #当前修改过的文件

find ~ -newer /home/pzdn/Code #列出home下比Code还要新的文件 ly

```

>-exec选项解释：

后面是一个命令，作用到每一个查找到的结果。必须以分号结尾——\;，字符串{}将用find命令搜索到的匹配的文件名来替换。

**命令别名 & 历史命令**

```

alias lm='ls -l|more' #设置别名

alias #查看所有的别名

unalias lm#取消别名

history #查看历史命令

history 10 #查看最新的10条

history -w #写入histfile中

echo $HISTSIZE

!! #发音：bang-bang

!3

!-3 #倒数第三条命令

!al

!?str #含有str的命令

^str1^str2 #将str1替换成str2，并执行

alias h='history'

```

# 5. 环境变量

环境指的是一个字典集合，name-value。

**PATH变量**

即命令的搜索路径。系统的环境变量一般从\/etc\/profile进行搜索。

**Profile**

用户可以在Profile文件中加入环境变量，比如ORACLE\_HOME,HOME...这样重新登录之后，这些环境变量都会得以设置，不用每次都手工设置。

Unix\/Linux有两个profile文件：

> 1.\/etc\/profile:是全局profile文件，设置后会影响到所有用户

>

> 2.\/home\/username\/.profile或.bash\_profile是针对特定用户的，可以针对用户，来配置自己的环境变量。

>

> note:profile是unix上才有的;bash\_profile是Linux下有的\(Linux下，用户目录没有.profile文件\)\/home\/username\/.profile或.bash\_profile，都是隐藏文件，需要使用ls -a才能看到。

**执行顺序**

Bash登陆\(login\)的时候，Profile执行的顺序

1. 先执行全局Profile, \/etc\/profile

2. 接着bash会检查使用者的HOME目录中，是否有 .bash\_profile 或者 .bash\_login或者 .profile，若有，则会执行其中一个，执行顺序为：

.bash\_profile 最优先 &gt; .bash\_login其次 &gt; .profile 最后。

**export &lt;= env &lt;= set**

* export 显示从 Shell 中导出成环境变量的变量，也能通过它将自定义变量导出为环境变量

* env 当前用户的，即可以覆盖从父Shell继承而来的变量；

* set显示当前 Shell 所有环境变量，包括其内建环境变量（与 Shell 外观等相关），用户自定义变量及导出的环境变量

```

# 定义环境变量、修改PATH、立即生效（常用）

sudo vim /etc/profile

export HIVE_HOME=/app/hive-0.12.0 #将HIVE_HOME添加到环境中

export PATH=$PATH:$HIVE_HOME/bin #修改PATH

export CLASSPATH=$CLASSPATH:$HIVE_HOME/bin #修改CLASSPATH

source /etc/profile #让文件立即生效

echo $PATH #显示最终结果

#打印环境变量的值

export -p #打印

env -i PATH=$PATH HOME=$HOME … # run a program in a modified environment，-i 用于初始化，即重新复制，之后将会覆盖继承的export。

#比较三者的区别

export | export.txt #out export

env | env.txt #out env

set | set.txt #out set

vimdiff export.txt env.txt set.txt #compare

```

# 6. 机器管理

```

reboot #重启

poweroff #立马关机

```
