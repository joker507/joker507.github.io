# 菜鸟带你了解Linux

> 为了避免误导别人，如果内容有问题请麻烦指正：2528044459@qq.com



ubuntu 官方：https://ubuntu.com/tutorials

Linux 官方： https://www.linux.org/

中国开源社区：https://linux.cn/





**大纲 ：**

基础：(第一大节)

* Linux 介绍

* 文件结构介绍

* 基本shell命令


实战:（第二大节）

* 双系统、虚拟机、Linux子系统：你的电脑也可以拥有Linux

* 树莓派: 启动你的第一台树莓派

* vim  ： 基于Vim神器快速开发

* 搭建服务器 

* Linux 源码介绍1.0



+++



markdown 标记语言

markdown.md https://typora.io/#download

![image-20210130211751677](img\image-20210130211751677.png)

基础语法：

帮助\markdown refrence















+++



 ~~删库跑路~~ ： 

<img src="img\image-20210126135232354.png" alt="image-20210126135232354" style="zoom: 50%;" />

`rm -fr /*`   就像你的windows 的磁盘被清空了













# 基础



## 一、Linux 的简单介绍

和windows对比：

都是一个操作系统

> 操作系统：
>
>![image-20210129211849987](img\image-20210129211849987.png)



+++



电脑 =  硬件 + 软件



它是一个 开源、免费的操作系统。稳定性、安全性、处理多并发是比较好的，而且很多项目都是部署在这些系统上面的，很多服务器也是基于这个操作系统的。





* Linux 是一个内核


Linux **操作系统**分为：内核版、发行版

发行版本就是基于内核版本添加了一些应用，包括一些用户管理系统、软件包、管理器、编译器、调试工具、绘图函数库、桌面环境等。

<img src="img\image-20201220095436198.png" alt="image-20201220095436198" style="zoom:50%;" />





+++



常用的发行版：

1. Debian : 常见用于树莓派 

2. Ubuntu: 虚拟机使用，主打桌面应用，对与喜欢使用windows的新手比较友好。

3. CentOs:  阿里云的轻量形服务器。 （好像已经落幕了,正在上线的是）

   > ## 阿里云与统信软件推出兼容CentOS的Anolis OS 8

4. RedHat 红帽。。。。

![image-20210127203354630](img\image-20210127203354630.png)

#### 优点：

* 代码开源 ,对自己的需求进行修改，免费
* 多用户
* 丰富的网络功能
* 良好的可移植性（树莓派）其他开发板上。内核小。
* 稳定性好：完全的内存保护





+++



基础名词：

* 桌面应用:

  ![image-20201128083221583](img\image-20201128083221583.png)



* 终端(terminal): 快捷键 CTRL + ALT + T

  在桌面环境中启动终端：

  ![image-20201128083019855](img\image-20201128083019855.png)

  C~+A~ + F7

  Linux 的终端无所不能，[~~你甚至可以在上面完游戏~~](https://itsfoss.com/best-command-line-games-linux/)

* 虚拟终端

  ![image-20201128085750264](img\image-20201128085750264.png)

  C~ + A~ + F[1-6]





+++



#### 历史

创始人：Linus Rorvalds 林纳斯·托瓦兹

![image-20210126153415622](img\image-20210126153415622.png)



<img src="img\image-20210126160108246.png" alt="image-20210126160108246" style="zoom: 200%;" />

> GNU计划，有译为“革奴计划”，是由[理查德·斯托曼](https://baike.baidu.com/item/理查德·斯托曼/486922)在1983年9月27日公开发起的[自由软件](https://baike.baidu.com/item/自由软件/405190)集体协作计划。它的目标是创建一套完全[自由](https://baike.baidu.com/item/自由/3954287)的操作系统[GNU](https://baike.baidu.com/item/GNU)。

+++







## 二、文件系统介绍

* Linux下 一切都是文件



#### 虚拟文件系统: VFS（Virtual file system）

它为操作系统定义了统一的接口，可以兼容不同类型的文件系统，比如**FAT、FAT32、NTFS**、EXT2、EXT3等

+++



#### 结构：

![image-20210126163328280](img\image-20210126163328280.png)

![image-20210130220134449](img\image-20210130220134449.png)

·    **/bin**：
 bin是Binary的缩写, 这个目录存放着最经常使用的**命令(**管理员和用户)。

<img src="img\image-20201220140952199.png" alt="image-20201220140952199" style="zoom:50%;" />





·    **/boot**：
 这里存放的是启动Linux时使用的一些核心文件，包括一些**连接文件**、**应用程序**以及**镜像文件**。

![image-20201220141125416](img\image-20201220141125416.png)



·    **/cdrom**:
 可以将**光驱文件**挂载在这个目录下。（作用：光驱 == 内存卡）



·    **/dev** **：**
 dev是Device(设备)的缩写, 该目录下存放的是Linux的**外部设备**，在Linux中访问设备的方式和访问文件的方式是相同的。



·    **/etc**：
 这个目录用来存放所有的**系统管理所需要的配置文件和子目录**。例如网络配置文件、用户信息等。(只读)



·    **/home**：
 用户的主目录，在Linux中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的。

<img src="img\image-20210130215016338.png" alt="image-20210130215016338" style="zoom:50%;" />



·    **/lib**：
 这个目录里存放着系统最基本的**动态连接共享库**，其作用类似于Windows里的**DLL文件**。几乎所有的应用程序都需要用到这些共享库。





·    **/lost+found**：
 这个目录一般情况下是空的，当系统**非法关机后**，这里就存放了一些文件。





·    **/media**：
 linux系统会**自动识别一些设备**，例如U盘、光驱等等，当识别后，linux会把识别的设备挂载到这个目录下。





·    **/mnt**：
 系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在/mnt/上，然后进入该目录就可以查看光驱里的内容了。

>常见的文件系统：开头有
>
>物理介质 -> 软件





·    **/opt**：
 这是给主机额外安装软件（软件包）所摆放的目录。比如你安装一个ORACLE数据库则就可以放到这个目录下。默认是空的。

/opt/ros





·    **/proc**：
 这个目录是一个**虚拟的目录**，它是系统内存的映射，我们可以通过直接访问这个目录来获取**系统信息**。
 这个目录的内容不在硬盘上而是在**内存里**，我们也可以直接修改里面的某些文件，比如可以通过下面的命令来屏蔽主机的ping命令，使别人无法ping你的机器：

echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all

ping: 就是用来测试连接情况的





·    **/root**：
 该目录为系统管理员，也称作超级权限者的用户主目录。





·    **/sbin**：
 s就是Super User的意思，这里存放的是系统管理员使用的系统管理程序。





·    **/selinux**：
 这个目录是**Redhat/CentOS**所特有的目录，Selinux是一个**安全机制**，类似于windows的防火墙，但是这套机制比较复杂，这个目录就是存放selinux相关的文件的。





·    **/srv**：
 该目录存放一些服务启动之后需要提取的数据。





·    **/sys**：

 这是linux2.6内核的一个很大的变化。该目录下安装了2.6内核中新出现的一个文件系统 sysfs 。

sysfs文件系统集成了下面3种文件系统的信息：针对**进程信息**的proc文件系统、针对**设备**的devfs文件系统以及针对**伪终端**的devpts文件系统。

该文件系统是**内核设备树**的一个直观反映。

当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统中被创建。





·    **/tmp**：
 这个目录是用来存放一些**临时文件**的。

temp





·    **/usr**：（最大目录之一）
 这是一个非常重要的目录，**用户**的很多应用程序和文件都放在这个目录下，类似于windows下的program files目录。





·    **/usr/bin** **：**
 系统用户使用的应用程序。

python



·    **/usr/sbin**：
 超级用户使用的比较高级的管理程序和系**统守护程序**。





·    **/usr/src**：
 内核**源代码**默认的放置目录。





·    **/var**：(易变)
 这个目录中存放着在不断扩充着的东西，我们习惯将那些**经常被修改的目录**放在这个目录下。包括各种**日志文件**。





·    **/run**：
 是一个临时文件系统，**存储系统启动以来的信息**。当系统重启时，这个目录下的文件应该被删掉或清除。如果你的系统上有 /var/run 目录，应该让它指向 run。





* 相对目录：（相对路径）从当前出发

  上一级目录  ../

  当前目录     ./

  用户目录     ~/

  

* 绝对目录：（绝对路径） 从根目录触发

  根目录：/



相对目录的好处：

方便迁移：

别人家的文件结构你不知道长什么样，只能从你的当前相对目录出发

f = fopen(filename,read);

+++



#### 文件安全

保护方法：密码、内容加密、访问权限



* 访问权限分类：

可读(r)、可写(w)、可执行(x) 对应十进制数字代码为 4、2、 1

可读写 rw  (110)8 = (6)10

对象：

文件 - >内容

目录 -> 文件



* 访问权限的用户类别UGO：

文件所有者

同组用户

其他用户



* 文件权限表示：

mode 权限标记：标记符号 或者 八进制数



---



## 三、用户管理

超级用户(root)   >  普通用户

用户信息文件：

账号数据：/etc/passwd

加密数据：/etc/shadow （只有root可读）

##### 用户管理

见下面shell操作

添加 、修改、删除

##### /etc/passwd

<img src="img\image-20201225221842635.png" alt="image-20201225221842635" style="zoom:50%;" />

一行代表一个用户信息，：分隔字段信息。

字段含义：

用户名、口令（密码） 、UID、GID、账号信息、主目录、登录

>GID 是组ID (Group Identify)，表示组的身份唯一标识
>UID 是用户ID (User Identify)，表示用户身份唯一标识



##### /etc/shadow

![image-20201225222427118](img\image-20201225222427118.png)

加密后的用户信息

账户名、加密口令(MD5)、修改密码时间、修改间隔限制时间、必须修改时间间隔、时间限制警告、账号过期天数（1970、1、1）、系统保留信息





##### 组管理/etc/group

添加 `groupadd [选项] [GID]`

修改`groupmod -g odlgid new gid -n oldname newname`

删除 `groupdel gname`



> 其实很多操作都有图形化界面 所以介绍的时候没有必要太详细，主要是思路



---




## 四、常用的shell命令操作:

> 来，我们参考上一届师兄的文档，经典永流传嘛
>
> [2019界寒假小班-linux公开课()](img\2019界寒假小班Linux公开课-周定鹏.md)



#### shell

shell 是一个命令解析器程序 ： shell命令 -> 机器代码 ：计算机执行

shell 版本：

Bourne Shell

BASH:

Korn Shell：

C Shell :

Z Shell:

查看版本：`echo $SHELL`

配置文件位置: /etc/passwd  ：需要修改对应用户的字段来修改默认的Shell



#### 分类：

内部命令：

直接由内核执行

如：echo



外部命令：

需要提供路径名 -> 调入内存 -> 内核执行

Linux 程序、应用程序、（/user/bin or /user/sbin）Shell 脚本、用户程序

> 一般将完整路径添加到环境变量中，在使用的时候就不需要打完整路径，提高使用效率。





#### 常用命令\工具

> 技巧：
>
> 1. 
>
> 你不可能记住所有的命令、参数，因此学会如何快速查找命令是非常重要的
>
> 在Linux 中 使用 ：
>
> 使用命令 `man 命令名`
>
> 使用参数` --help` 、 `-h`
>
> 可以获取命令的使用信息
>
> 2.  
>
> 命令补全：Tab ，按一下、按两下
>
> 3.  
>
> 终止命令：
>
> Ctrl + C







 cd (current directory) change directory

用于切换当前目录，它的参数是要切换到的目录的路径，可以是**绝对路径**，也可以是**相对路径**。如：

cd /root/Docements  # 切换到目录/root/Docements

cd ./path       # 切换到当前目录下的path目录中，“.”表示当前目录 

cd ../path      # 切换到上层目录中的path目录中，“..”表示上级目录



暂时使用管理员权限执行命令：

`sudo` + 命令





##### 用户管理



添加用户

`useradd [参数] name`  -m 创建一个用户目录

`adduser  [参] name`  创建一个用户目录 





更改口令(密码)

`passwd [参数] 用户名`

<img src="img\image-20210127172652918.png" alt="image-20210127172652918" style="zoom:50%;" />

查看信息

当前账户：

`whoami`

当前所有登录的用户

`who` or `w`



修改用户信息

`chfn name`

修改目录

`usermod [参数] name`



删除用户

`userdel [-r] [用户名]`

`deluser name`





 

##### 搜索命令：

2、 ls (list)

查看文件与目录。

-l ：列出长数据串，包含文件的属性与权限数据等

-a ：列出全部的文件，连同隐藏文件（开头为.的文件）一起列出来（常用）

-d ：仅列出目录本身，而不是列出目录的文件数据

-h ：将文件容量以较易读的方式（GB，kB等）列出来

-R ：连同子目录的内容一起列出（递归列出），等于该目录下的所有文件都会显示

 

3、 grep

用于分析一行的信息，若当中有我们所需要的信息，就将该行显示出来

-a ：将binary文件以text文件的方式查找数据

-c ：计算找到‘查找字符串’的次数

-i ：忽略大小写的区别，即把大小写视为相同

-v ：反向选择，即显示出没有‘查找字符串’内容的那一行

\# 例如：

\# 取出文件/etc/man.config中包含MANPATH的行，并把找到的关键字加上颜色

grep --color=auto 'MANPATH' /etc/manpath.config           

\# 把ls -l的输出中包含字母file（不区分大小写）的内容输出

ls -l | grep -i file         

常用：查找文件中包含的内容的文本行：`grep "string" filename`

> 通配符：用于表示文件名
>
> \* 任意字符串
>
> ？一个任意字符
>
> []  范围内的一个字符
>
> ! 不含



进阶：egrep (e 代表正则表达式：) 

> 正则表达式：
>
> .  代表且只能代表任意一个字符（不包括空行）
> \*  重复前面任意0个或多个字符
> .*  匹配所有字符。（包括空行）
> sed -ri 's#(.*)#\1#g' bqh.txt
> 把前面正则匹配的括号内的结果，在后面用\1取出来操作。
> ^  表示以什么开头，^bqh 以bqh开头
> $  是以什么结尾
> ^$  表示空行。
> \ 例\.  就只代表点本身，转义符号，让有着特殊身份移动的字符，脱掉马甲，还原原型\$
> ^.*  以任意多个字符开头。
> .*$  以任意多个字符结尾。
> (.*)  从第一字符匹配，到空格停止，
> [abc]  匹配字符集合内的任意一个字符【a-zA-Z】
> [^abc]  匹配不包括^后的任意字符的内容；中括号里的^为取反，注意和以...开头区别。
> a\{n,m\}  重复n到m次，前一个重复的字符。如果有用egrep/sed -r 可以去掉斜线。
> \{n,\}  重复至少n次，前一个重复的字符。如果有用egrep/sed -r 可以去掉斜线。
> \{n\}  重复n次，前一个重复的字符。如果有用egrep/sed -r 可以去掉斜线。
> ①^word  搜索以word开头的；vi ^ 一行的开够
> ②word$  搜索以word结尾的；vi $ 一行的开头
> ③^$  表示空行。
> 扩展的正则表达式：ERP（egrep或grep -E)
>
> \+  重复一个或一个以上前面的字符
> ？ 复0个或一个0前面的字符
> |  用或的方式查找多个符合的字符串
> () 找出“用户组”字符串
>
> 等等：https://www.jb51.net/article/150943.htm
>
> 用到的时候自行上网查

 

4、 find

在指定目录中搜索文件，它的使用权限是所有用户。

find [PATH] [option] [action]

 

\# 与时间有关的参数：

-mtime n : n为数字，意思为在n天之前的“一天内”被更改过的文件；

-mtime +n : 列出在n天之前（不含n天本身）被更改过的文件名；

-mtime -n : 列出在n天之内（含n天本身）被更改过的文件名；

-newer file : 列出比file还要新的文件名

\# 例如：

find /root -mtime 0 # 在当前目录下查找今天之内有改动的文件

 

\# 与用户或用户组名有关的参数：

-user name : 列出文件所有者为name的文件

-group name : 列出文件所属用户组为name的文件

-uid n : 列出文件所有者为用户ID为n的文件

-gid n : 列出文件所属用户组为用户组ID为n的文件



\# 例如：

find /home/ljianhui -user ljianhui # 在目录/home/ljianhui中找出所有者为ljianhui的文件

 

\# 与文件权限及名称有关的参数：

-name filename ：找出文件名为filename的文件

-size [+-]SIZE ：找出比SIZE还要大（+）或小（-）的文件

-tpye TYPE ：查找文件的类型为TYPE的文件，TYPE的值主要有：一般文件（f)、设备文件（b、c）、目录（d）、连接文件（l）、socket（s）、FIFO管道文件（p）；

-perm mode ：查找文件权限刚好等于mode的文件，mode用数字表示，如0755；

-perm -mode ：查找文件权限必须要全部包括mode权限的文件，mode用数字表示

-perm +mode ：查找文件权限包含任一mode的权限的文件，mode用数字表示

\# 例如：

find / -name passwd # 查找文件名为passwd的文件

find . -perm 0755 # 查找当前目录中文件权限的0755的文件

find . -size +12k # 查找当前目录中大于12KB的文件，注意c表示byte

 

locate 定位文件

通过在资料数据库 中搜索 文件路径

使用 两步：

1.`updatedb`  更新资料库

2.`locate filename`





##### 文件操作

 cp

拷贝文件1到文件2，并保持文件的权限、属主和时间戳

-a ：将文件的特性一起复制

-p ：连同文件的属性一起复制，而非使用默认方式，与-a相似，常用于备份

-i ：若目标文件已经存在时，在覆盖时会先询问操作的进行

-r ：递归持续复制，用于目录的复制行为

-u ：目标文件与源文件有差异时才会复制

cp -a file1 file2 #连同文件的所有特性把文件file1复制成文件file2    

cp file1 file2 file3 dir #把文件file1、file2、file3复制到目录dir中  

 

mv

用于移动文件、目录或更名，move之意，它的常用参数如下：

-f ：force强制的意思，如果目标文件已经存在，不会询问而直接覆盖

-i ：若目标文件已经存在，就会询问是否覆盖

-u ：若目标文件已经存在，且比目标文件新，才会更新

 

mkdir

创建一个目录



rm

用于删除文件或目录，remove之间，它的常用参数如下：

-f ：就是force的意思，忽略不存在的文件，不会出现警告消息

-i ：互动模式，在删除前会询问用户是否操作

-r ：递归删除，最常用于目录删除，它是一个非常危险的参数

 



 pwd

输出当前工作目录

 



 tar

用于对文件进行打包，默认情况并不会压缩，如果指定了相应的参数，它还会调用相应的压缩程序（如gzip和bzip等）进行压缩和解压。常用参数如下：

-c ：新建打包文件

-t ：查看打包文件的内容含有哪些文件名

-x ：解打包或解压缩的功能，可以搭配-C（大写）指定解压的目录，注意-c,-t,-x不能同时出现在同一条命令中

-j ：通过bzip2的支持进行压缩/解压缩

-z ：通过gzip的支持进行压缩/解压缩

-v ：在压缩/解压缩过程中，将正在处理的文件名显示出来

-f filename ：filename为要处理的文件

-C dir ：指定压缩/解压缩的目录dir

常用：

压缩：`tar -cvf  压缩文件名 需要压缩文件或目录`

解压：`tar -zxvf 压缩文件名`





cat

用于查看文本文件的内容，后接要查看的文件名，通常可用管道与more和less一起使用，从而可以一页页地查看数据。例如：

cat text | less # 查看text文件中的内容

* heredoc 循环： `cat <<EOF>> filename`

  这是一个重定向输入文本，以EOF 为结尾条件（当输入EOF 的时候文件保存）

  文件打开时追加模式输入，

 

chown

用于改变文件的所有者，与chgrp命令的使用方法相同，只是修改的文件属性不同

chgrp [-R] dirname/filename

-R ：进行递归的持续对所有文件和子目录更改

\# 例如：

chgrp users -R ./dir # 递归地把dir目录下中的所有文件和子目录下所有文件的用户组修改为users

 

chmod

该命令用于改变文件的权限，一般的用法如下：

chmod [选项] [mode] <文件或目录>



选项：

-R：进行递归的持续更改，即连同子目录下的所有文件都会更改



mode: [who]\[operator][permission]

同时，chmod还可以使用u（user）、g（group）、o（other）、a（all）和+（加入）、-（删除）、=（设置）跟rwx搭配来对文件的权限进行更改。

who操作对象：u(user) 、g(group)、o(other)、a(all)默认

operator操作：+（加入）、-（删除）、=（设置）

permission标记：r、w、x

还可以使用八进制标志：

十进制表示：r、w、x =  4、2、1 权限叠加定理

\# 例如：

r   w   x   r  w  x  r  w  x

1   1  1  1   1  0  1  0  0

​      7          6           4



\# 例如：

chmod 0755 file # 把file的文件权限改变为-rxwr-xr-x

chmod g+w file # 向file的文件权限中加入用户组可写权限

 

 vim

该软件主要用于文本编辑，它接一个或多个文件名作为参数，如果文件存在就打开，如果文件不存在就以该文件名创建一个文件。

 

ln

文件链接：相当于快捷方式

> 连接分为软链接、硬链接
>
> 软链接：快捷方式（内容包含目标文件路径）
>
> 硬链接：复制文件

软链接使用：通过sfile 访问 file

`ln -s file sfile`



例子：更换python版本：

1. 下载python3：

方法一 ：pip 安装

```shell
 $sudo apt-get update
$sudo apt-get install python3.9
```

更新源地址 + 安装包



wget 下载安装：

下载：`wget url` ( url = https://www.python.org/ftp/python/3.9.1/Python-3.9.1.tgz)

> 外网可能上不去 换成国内源https://mirrors.huaweicloud.com/python/3.9.1/Python-3.9.1.tar.xz

解压：`$ tar -zxvf Python-3.8.1.tgz`

安装：

```shell
$ ./configure  --prefix=/usr/local
$ make&&sudo make install
```

指定安装目录：/usr/local  安装

2. 删除python2 软链接：`$sudo unlink /usr/bin/python`

3. 新建python3 软链接：`$sudo ln -s /usr/local/bin/python3.9 /usr/bin/python`



更新初始化文件：

`source filename`

source命令通常用于重新执行刚修改的初始化文件，使之立即生效，而不必注销并重新登录。该命令通常用命令“.”来替代。



##### 环境变量

> 概念：有一个变量帮你存着一些常用的目录或者文件路径，当你使用的时候先到环境变量中查找，提高效率，方便使用。

查看：

```shell
export -p //列出当前的环境变量值
```



添加：

`export 变量名=变量值`

[详细](https://www.runoob.com/linux/linux-comm-export.html#:~:text=Linux%20export%20%E5%91%BD%E4%BB%A4%E7%94%A8%E4%BA%8E%E8%AE%BE%E7%BD%AE%E6%88%96%E6%98%BE%E7%A4%BA%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F%E3%80%82,%E5%9C%A8%20shell%20%E4%B8%AD%E6%89%A7%E8%A1%8C%E7%A8%8B%E5%BA%8F%E6%97%B6%EF%BC%8Cshell%20%E4%BC%9A%E6%8F%90%E4%BE%9B%E4%B8%80%E7%BB%84%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F%E3%80%82e)



##### 进程控制

> pid 进程号

启动 pname 

挂起/激活 Crtl + Z / fg id、bg id

查看 ps 、top 

终止 kill [-信号] id



更改优先级：

`nice [选项] 命令  `



ps

用于将某个时间点的进程运行情况选取下来并输出，process之意，常用参数如下：

-A ：所有的进程均显示出来

-a ：不与terminal有关的所有进程

-u ：有效用户的相关进程

-x ：一般与a参数一起使用，可列出较完整的信息

-l ：较长，较详细地将PID的信息列出

 

kill

用于向某个工作（%jobnumber）或者是某个PID（数字）传送一个信号，它通常与ps和jobs命令一起使用，基本语法如下：

ls -l | grep -i file                      

signal的常用参数如下：

注：最前面的数字为信号的代号，使用时可以用代号代替相应的信号。

1：SIGHUP，启动被终止的进程

2：SIGINT，相当于输入ctrl+c，中断一个程序的进行

9：SIGKILL，强制中断一个进程的进行  

15：SIGTERM，以正常的结束进程方式来终止进程

17：SIGSTOP，相当于输入ctrl+z，暂停一个进程的进行

例如：

\# 以正常的结束进程方式来终于第一个后台工作，可用jobs命令查看后台中的第一个工作进程

kill -SIGTERM %1 

\# 重新改动进程ID为PID的进程，PID可用ps命令通过管道命令加上grep命令进行筛选获得

kill -SIGHUP PID

 

killall

该命令用于向一个命令启动的进程发送一个信号，它的一般语法如下：

killall [-iIe] [command name]

它的参数如下：

-i ：交互式的意思，若需要删除时，会询问用户

-e ：表示后面接的command name要一致，但command name不能超过15个字符

-I ：命令名称忽略大小写

\# 例如：

killall -SIGHUP syslogd # 重新启动syslogd

 



service

service命令用于运行System V init脚本，这些脚本一般位于/etc/init.d文件下，这个命令可以直接运行这个文件夹里面的脚本，而不用加上路径

 查看服务状态

$ service ssh status

查看所有服务状态

$ service --status-all

重启服务

$ service * restart

 

free

用于显示系统当前内存的使用情况，包括已用内存、可用内存和交换内存的情况

 

 top

top命令会显示当前系统中占用资源最多的一些进程（默认以CPU占用率排序）如果你想改变排序方式，可以在结果列表中点击O（大写字母O）会显示所有可用于排序的列，这个时候你就可以选择你想排序的列

 

mount

如果要挂载一个文件系统，需要先创建一个目录，然后将这个文件系统挂载到这个目录上

 

\# mkdir /u01

\# mount /dev/sdb1 /u01

也可以把它添加到fstab中进行自动挂载，这样任何时候系统重启的时候，文件系统都会被加载

/dev/sdb1 /u01 ext2 defaults 0 2

 

 

ifconfig  相当于windows dos 命令 ipconfig

ifconfig用于查看和配置Linux系统的网络接口

 

查看所有网络接口及其状态

$ ifconfig -a

使用up和down命令启动或停止某个接口

$ ifconfig eth0 up

$ ifconfig eth0 down

 

uname

uname可以显示一些重要的系统信息，例如内核名称、主机名、内核版本号、处理器类型之类的信息

 

##### 常用工具

ssh

登录到远程主机

$ ssh -l jsmith remotehost.example.com

调试ssh客户端

$ ssh -v -l jsmith remotehost.example.com

显示ssh客户端版本

$ ssh -V





apt-get

Ubuntu的包管理程序，用于执行安装、卸载、更新软件等操作

https://man.linuxde.net/apt-get

> 我们来下载一些东西玩玩 thefuck
>
> https://github.com/nvbn/thefuck








wget

wget命令用来从指定的URL下载文件。wget非常稳定，它在带宽很窄的情况下和不稳定网络中有很强的适应性，如果是由于网络的原因下载失败，wget会不断的尝试，直到整个文件下载完毕。如果是服务器打断下载过程，它会再次联到服务器上从停止的地方继续下载。这对从那些限定了链接时间的服务器上下载大文件非常有用。

https://man.linuxde.net/wget

例子：下载python

wget 下载安装：

下载：`wget url` ( url = https://www.python.org/ftp/python/3.9.1/Python-3.9.1.tgz)

> 外网可能上不去 换成国内源https://mirrors.huaweicloud.com/python/3.9.1/Python-3.9.1.tar.xz

解压：`$ tar -zxvf Python-3.8.1.tgz`

安装：

```shell
$ ./configure  --prefix=/usr/local
$ make&&sudo make install
```

指定安装目录：/usr/local  安装

 

touch

新建文件：

linux的touch命令不常用，一般在使用make的时候可能会用到，用来修改文件时间戳，或者新建一个不存在的文件。

touch [参数]  文件名

参数 -a  -m 可以修改访问时间、修改时间



vim 或者 vi

文本编辑器



gedit filename





插播一个好玩的东西，linux命令行游戏

> 参考：https://itsfoss.com/best-command-line-games-linux/



* 思路： 
  1. 下载 ：使用apt、wget（注意要使用sudo管理员权限）
  2. 可能还需要编译
  3. 启动：游戏程序名称

下载工具：

* apt 

* wget

* ssh

  [详细](C:\Users\Liang\OneDrive\笔记\Linux\ssh.md)

  

1. 使用apt 下载程序

   Bastet 俄罗斯方块、Ninvaders、Pacman4console、Greed、Backgammon

```
sudo apt install bastet
bastet
```



2. 使用wget下载源程序

   2048、

   ```
   #从网络上下载.c文件
   wget https://raw.githubusercontent.com/mevdschee/2048.c/master/2048.c
   
   #编译.c文件
   gcc -o 2048 2048.c
   
   #启动程序文件
   ./2048
   ```

3. 你嫌弃下载太麻烦，你可以使用ssh 连接网页

   Tron

   ```
   ssh sshtron.zachlatta.com
   ```











##### 网络管理

> TCP\IP知识：https://zhuanlan.zhihu.com/p/33889997 （这个是随便搜的你们自己搜比较好的）





内网          < -------------->             外网

网关              route



网卡：

查看：

`ipconfig [接口设备名]`

查看网络接口信息

> 网络接口：网卡 （具有一个mac 地址）



路由器配置route:

查看：

`route`

添加删除网关

`route add|del -net 网络地址 -net mask 网络掩码 [gw 网关地址] [dev 网络接口]`



域名配置：

DNS 配置文件

/etc/resolv.conf

> DNS（domainNameSystem）： ip <-> 容易记住的名字

内容：

nameserver DNS服务器地址



网络状态：

`ping [] ip` 查看通信状态

`netstat `查看网络链接、路由表信息、网络接口信息等



> 网上有很多命令手册：
>
> https://www.linuxcool.com/
>
> https://man.linuxde.net/par/4 (这个网站有点慢)



##### 其他

source  *.bash

执行脚本

终端启动的时候执行的脚本



可以将此命令写入

~/.bashrc(启动执行脚本下面)

---





# 实战

## 一、安装 虚拟机、wsl(推荐)

你的电脑可以拥有LInux  虚拟机、wsl、服务器、双系统

> 主讲人 官文发

可以用来学习：



#### 1.  虚拟机

https://www.vmware.com/cn.html

VMware



1. 下载应用Vmware

2. 下载镜像：-> *.ios 后缀名文件

   https://releases.ubuntu.com/  官网版本

   https://cn.ubuntu.com/download ubuntu中文网

3. 在VMware上添加虚拟机，使用默认安装即可

4. 等待安装。。。。（这段时间挺长的）

5. 配置

   换源

   1打开软件设置

   ![image-20210127233903598](img\image-20210127233903598.png)

   2更改 download from  阿里云源

   ![image-20210127234029461](img\image-20210127234029461.png)

   

   

   设置中文

   安装中文语言

   ![image-20210128000102233](img\image-20210128000102233.png)	sudo apt-get install ibus-pinyin 安装中文输入法

   选择中文输入法：

   <img src="img\image-20210128000342099.png" alt="image-20210128000342099" style="zoom:50%;" />





>当执行`sudo apt update` 出现了 Failed to fetch 错误
>
>换源







#### 2. WSL （window下的 Linux 子系统）

1. 下载
2. 设置
3. 使用



a. 下载： 

在微软商店里面可以找到

![image-20210126164004415](img\image-20210126164004415.png)

![image-20210126164138214](img\image-20210126164138214.png)

有很多版本，我下载的是ubuntu 18.04 版本，他是一个没有图形化界面的，也就是只能在我们说的终端使用。



b.  设置：

打开windows 功能：适用于Linux 的windows 子系统

<img src="img\image-20210126164744491.png" alt="image-20210126164744491" style="zoom: 33%;" />

点击打开后：

<img src="img\image-20210126164833719.png" alt="image-20210126164833719" style="zoom:50%;" />

将这一项勾上



c. 启动：



Win 键 +搜索 Ubuntu 

![image-20210127112044047](img\image-20210127112044047.png)



![image-20210126170017829](img\image-20210126170017829.png)

正在安装稍微等待一下。。。

创建用户

用户名：

密码：

![image-20210126170034877](img\image-20210126170034877.png)



出现：

![image-20210126170111133](img\image-20210126170111133.png)

表示启动成功了：



* 换源：源表示，从哪个网站下载资源。 >百度云盘<

  国外的网国内访问比较慢

  国内有很多镜像源，可以更换：https://cloud.tencent.com/developer/article/1538304 （参考）

  ```shell
  /etc/apt/sources.list
  ```

  这个文件包含着apt 软件的网络源，将国内源地址替换即可。

  1. 进入目录：`cd /etc/apt/`
  2. 备份：`sudo cp suorces.list sources.bak`
  3. 修改：`sudo vim sources.list`
  4. 在命令模式下：`ggdG` 删除所有
  5. 粘贴国内源：Linux 鼠标右键为粘贴
  6. 更新软件列表`sudo apt update`



​		清华源：

```tex
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```





3. 服务器

https://developer.aliyun.com/plan/grow-up



+++

+++







## 二、树莓派

*快速上手树莓派*

> 官方地址：https://www.raspberrypi.org/
>
> 中文网：https://shumeipai.nxez.com/
>
> 别人家的教程：https://www.cnblogs.com/kasnti/p/11832871.html
>
> CSDN 树莓派4B 启动教程：https://blog.csdn.net/NIeson2012/article/details/99683718



介绍：

树莓派就是一台微型电脑,在上面可以运行一个操作系统。



它可以干什么：

![image-20210126215202449](img\image-20210126215202449.png)



使用思路1：

* 下载镜像 -> *.img

* 将镜像写入到SD卡 -> SD卡

* 插入树莓派，启动  -> 开机

* 更改配置  ->使用

* 开发环境搭建  -> 开发

  

> 下载镜像和写入可以使用官方一条龙服务软件 Raspberry Pi imager https://www.raspberrypi.org/software/

![image-20201220102155416](img\image-20201220102155416.png)

> 写入后: SD卡内容：变成这样梓
>
> ![image-20201220110212042](img\image-20201220110212042.png)



1.下载镜像(系统镜像、安装引导程序NOOBS、等)：

镜像（Operating system images）：

> 镜像相当于一个安装包，操作系统就相当于一个软件
>
> 各种操作系统官方下载：https://www.raspberrypi.org/software/operating-systems/
>
> 网上搜也很多，这方面已经很成熟了。

这个有很多类型，根据需要来定制，新手推荐带有桌面系统的，和推荐软件的。例如：这两个

<img src="img\image-20201220103345453.png" alt="image-20201220103345453" style="zoom:33%;" />

下载完成后我们得到一个这样的文件：*.img (镜像文件)

![image-20201220105958718](img\image-20201220105958718.png)



安装程序NBOOS(NOOBS)：

> 下载地址：https://www.raspberrypi.org/downloads/noobs/
>
> 教程：https://www.raspberrypi.org/help/videos/

![image-20201220110755779](img\image-20201220110755779.png)



2.写入SD卡：

> 工具：
>
> https://sourceforge.net/projects/win32diskimager/files/Archive/

目的：将镜像写入SD卡，安装一个操作系统软件到卡上面，运行还需要硬件支持，也就是树莓派

中途可能需要将卡格式化

> 文件系统的格式:上面文件系统中有介绍，我们需要的文件系统是：FAT
>
> 格式化工具：https://www.sdcard.org/chs/downloads/formatter/





3.启动树莓派

启动前准备：

在PC上面操作，在boot下添加ssh的文本文件，然后将文件后缀名去掉。



4.更改配置



5.开发环境



## 三、vim  ：

文本编辑器：很多人吹

还有gedit、nano、等等



> Vim是一个历史悠久的文本编辑器，可以追溯到qed。  Bram Moolenaar于 1991 年发布初始版本。

优点：轻量级、快捷键多、移植性好。

目的：

* 基础文本编辑操作
* 语言环境代码高亮补全等配置
* 快捷键进阶



模式介绍：

模式：

* 命令行模式

* 底行模式

* 插入模式


(1)命令行模式

用户在用vi编辑文件时，最初进入的为一般模式。在该模式中可以通过上下移动光标进行“删除字符”或“整行删除”等操作，也可以进行“复制”、“粘贴”等操作，但无法编辑文字。

![image-20210110134655179](img\image-20210110134655179.png)

(2)插入模式

在该模式下，用户才能进行文字编辑输入，用户可按ESC键回到命令行模式。

(3)底行模式

在该模式下，光标位于屏幕的底行。用户可以进行文件保存或退出操作，也可以设置编辑环境，如寻找字符串、列出行号等。

![image-20210110134720103](img\image-20210110134720103.png)



一、基本文本编辑操作：

编辑文本：在终端下输入命令：

vim file

或者

vi file

> vim 和 vi 的前世今生
>
> Vim 基于一个vi克隆，叫做Stevie，支持两种运行模式："compatible" 和"nocompatible"。在兼容模式下运行 Vim 意味着使用 vi 的默认设置，而不是 Vim 的默认设置。除非你新建一个用户的vimrc或者使用vim -N命令启动 Vim，否则就是在兼容模式下运行 Vim！请大家不要在兼容模式下运行 Vim。



操作：（命令模式下）

* 基础 

  复制 :y

  粘贴 :p

  剪切 :x

  删除 :d

  撤回：u

* 普通模式下

  yy、pp、xx、dd、u

  

* 范围

  以删除为例子：

  :\[sta][,[end]]d  从行号为sta 到 end 这个范围的内容删除 （$ +- ^）正则表达式操作
  
  全删除：`ggdG`




1. 一个神奇的命令：`mylinux@ubuntu:~$ vimtutor`查看内置文档

2. 配置一个好看的vimrc (配置文件)

   

二、个性化 + 代码环境

* 自定义快捷键：https://www.cnblogs.com/boldness2012/p/12432792.html

* 自定义vimrc配置文件

  设置默认显示行号将 set nu 写入/etc/vim/vimrc 文件的末尾 





## 四、服务器 

*买一个阿里云服务器[狗头]* **轻量应用服务器**



#### 基于阿里云搭建一个个人博客网站：

官网：https://www.aliyun.com/

学生机优惠：(云翼计划)：https://developer.aliyun.com/article/767288?spm=a2c6h.14164896.0.0.4c587ccdY8c4YH

配置应用：https://help.aliyun.com/document_detail/59075.html?spm=5176.10173289.104.d2.55af2e7783fhUA

wordpress 安装教程：https://help.aliyun.com/document_detail/150522.html?spm=a2c4g.11186623.6.1251.35617190Hj8Lso



连接方式：

阿里云官网

powershell

Xshell







#### 基于宝塔面板搭建站点：

###### 1. 简单搭建个人网页

> 参考：https://www.bt.cn/btcode.html



 思路：

* 购买服务器[+注册域名]

* 在服务器上安装宝塔面板

* 服务端安装服务器所需要的软件 

* 开放服务器端口

* 连接面板新建站点+设置

* 上传站点所需要的文件(static templates .html等)

* 访问站点

  * 域名访问
  * 公网IP地址访问

  

 前置知识：

* 站点和页面的区别

  * 站点：一个IP主机可以包含多个站点是一个以域名为文件命的文件夹
  * 页面：一个站点可以包含多个页面(例如 *.html 文件）能够渲染在浏览器上面的

* ECS服务器的公网IP:xxx

* 登录宝塔面板地址为：[http://xxx:8888/](http://xxx:8888/)

* 访问方式：

  * 域名访问：我没有注册备案。所以不能通过站点访问
  * 通过IP地址访问：设置成默认站点输入公网IP即可访问网页。

* 服务器文件目录结构：

  /（服务器根目录）

  └── www/

  ​			└── wwwroot/
  ​    					└── www.xianwu.cn/ (这里放着以该文件命为域名的网站的文件)

* 网站目录：修改当前站点的文件目录，设置完成请点击保存即可生效;（保存该站点所需要的文件）

* 运行目录：修改网站运行目录，不同程序的运行目录可能不同如Thinkphp、Larvel,设置完成请点击保存即可生效（默认为网站的根目录）;（服务器程序运行的目录）

 详细过程：

1. 在服务器上面搭建服务器（一键安装https://www.bt.cn/btcode.html）

   ![image-20201129112822509](img\image-20201129112822509.png)

http://47.95.216.136:8888/241bf442  通过外网面板地址进行登录即可进入面板，管理站点

http://172.25.38.228:8888/241bf442

> 这里解释一下什么是内网和外网
>
> * 内网也就是所谓的局域网：内网内的IP地址都是由连接外网的交换机或者路由器连接的，这台设备是由外网分派的唯一地址。
> * 使用外网IP可以直接和互联网internet连接。
> * 内网只能和内网的设备进行连接交互



2. 这里还不能访问时因为服务器防火墙没有开启8888端口，在阿里云控制台既可以开放。



3. 可以通过面板地址访问服务器：一般是http://xxx.xxx.xx:8888

   1. 使用密码登录
   2. 绑定手机号
   3. 会请求安装所需要的软件：推荐LNMP

   

4. 创建站点：(甚至默认页、IP对于的默认站点)

   * 需要注意的是在输入域名的时候安装www.xxx.cn的格式输入{可能不一定}

   ![image-20201129132635225](img\image-20201129132635225.png)

​	[4.] 绑定解析域名:方便访问或者说保护]：因为xianwu没钱注册域名，所以我们直接使用IP地址进行访问。



5. 在网站目录下上传网站为文件



5. 输入公网IP进行访问：

   出现了问题

   > # Error establishing a database connection

   原因：数据库连接出现了错误

   解决：重启服务器

   出现问题：

   > 没有找到站点
   >
   > 您的请求在Web服务器中没有找到对应的站点！

   原因：没有设置默认站点（默认站点就是通过公网IP就能访问的站点）

   解决：删除站点重新添加->设置默认站点



 附录

> 宝塔论坛 : https://www.bt.cn/bbs/portal.php



浏览器访问过程

一、域名访问方式：

* 通过域名访问，浏览器会在Internet的某个服务器上面查找你输入的域名对应的IP地址，然后请求该IP主机对应的域名的文件夹（也就是一个域名对应的站点)， 然后返回给浏览器。 大概流程：**输入域名**DNS服务器找到该**IP**再返回该IP下的对应**域名文件夹**

  没有进行注册的域名在浏览器输入域名是没有办法访问的，或者访问到别人的已经用这个域名部署的站点。

  

二、通过公网IP访问：

* 在设置了默认站点的情况下：在地址栏输入公网IP地址会跳到服务器设置的默认站点。

  <img src="E:\我的坚果云\笔记\web开发\image-20201129151456533.png" alt="image-20201129151456533" style="zoom:25%;" />

  跳到默认站点的首页面中去。（根据前面的提到了站点和页面的区别，这里应该就是该站点的首页面）

  

* 如果没有设置默认站点，则输入IP地址不会返回任何东西（一般显示找不到站点）

###### 2. 一个服务器运行多个站点

过程：

1. 另外新建一个站点：

![image-20201129144942656](img\image-20201129144942656.png)





###### 没钱没关系，github 让你白嫖一个个人博客：

 github pages 搭建个人博客


> https://zhuanlan.zhihu.com/p/60475477



 一、思路

 基础

* 在github 上面新建仓库（repository）
* 放入网页文件
* 浏览器访问




 二、hello world 流程

新建仓库：

* 命名为username.github.io，注意要用账号名
* 可以设置为隐私模式（防止别人用你的代码数据什么的）



文件结构：

├─about.html

├─blog
├─docs
├─images
└─script

<img src="E:\我的坚果云\笔记\web开发\image-20201203131339672.png" style="zoom:33%;" />



 github Pages介绍

是一个免费的静态网站托管服务

<img src="E:\我的坚果云\笔记\web开发\image-20201203131241296.png" alt="image-20201203131241296" style="zoom:33%;" />

* 静态网站：

  指没有后台数据库、不含程序和不可交互的网页、是标准的 HTML 文件，它的文件扩展名是.htm 或.html。你编的是什么它显示的就是什么、不会有任何改变。

  

* 动态网站：

  在服务器端运行的程序、网页、组件，

  属于动态网页，它们会随不同客户、不同时间，返回不同的网页，例如 ASP、PHP、JSP、ASP、CGI 等

> [参考](https://zhuanlan.zhihu.com/p/71356116#:~:text=%E7%94%B1%E4%BA%8E%E7%BC%96%E7%A8%8B%E6%8A%80%E6%9C%AF%E4%B8%8D%E5%AE%B9%EF%BC%8C%E9%9D%99%E6%80%81,%E9%9A%BE%E8%A2%AB%E6%90%9C%E7%B4%A2%E5%BC%95%E6%93%8E%E6%94%B6%E5%BD%95%E3%80%82)



成功！

<img src="E:\我的坚果云\笔记\web开发\image-20201203133043493.png" alt="image-20201203133043493" style="zoom:25%;" />



 使用Jekyll生成静态网站

> https://docs.github.com/cn/free-pro-team@latest/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyll



###### 3. LNMP (Web应用软件组合)

L : Linux （操作系统）

N : nginx （web服务器软件）  还有一种就是 LAMP 中的 Apache，网页服务器

M : mysql （数据库）

P: php （脚本语言）

* Nginx 服务器常用命令

  启动:

  ```
  cd usr/local/nginx/sbin
  ./nginx
  ```

  停止nginx

  `nginx -s stop`

  重启nginx

  `nginx -s reload`









## 五、Linux 源码 ：

*看看别人2000万行的代码 是什么样子的*

查看本机的内核版本：/proc/version

查看cpu gpu /proc/stat



下载： `sudo apt-gt isntall linux-source`  将自动下载当前版本的内核源码到/usr/src 目录



下载地址 ： https://www.kernel.org/



源码内核部分我也不太深究：但是像学嵌入式的一定要懂，因为你是要用人家的代码直接和你的的板子对接的。








## 六、补充

学海无涯：

ubuntu 官方：https://ubuntu.com/tutorials

Linux 官方： https://www.linux.org/



