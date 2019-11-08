# Linux

## 系统目录结构

**系统启动必须：**

- **/boot：**存放的启动Linux 时使用的内核文件，包括连接文件以及镜像文件。

- **/etc：**存放**所有**的系统需要的**配置文件**和**子目录列表，**更改目录下的文件可能会导致系统不能启动。

- **/lib**：存放基本代码库（比如c++库），其作用类似于Windows里的DLL文件。几乎所有的应用程序都需要用到这些共享库。

- **/sys**： 这是linux2.6内核的一个很大的变化。该目录下安装了2.6内核中新出现的一个文件系统 sysfs 。sysfs文件系统集成了下面3种文件系统的信息：针对进程信息的proc文件系统、针对设备的devfs文件系统以及针对伪终端的devpts文件系统。该文件系统是内核设备树的一个直观反映。当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统中

**指令集合：**

- **/bin：**存放着最常用的程序和指令

- **/sbin：**只有系统管理员能使用的程序和指令。

**外部文件管理：**

- **/dev ：**Device(设备)的缩写, 存放的是Linux的外部设备。**注意：**在Linux中访问设备和访问文件的方式是相同的。

- **/media**：类windows的**其他设备，**例如U盘、光驱等等，识别后linux会把设备放到这个目录下。

- **/mnt**：临时挂载别的文件系统的，我们可以将光驱挂载在/mnt/上，然后进入该目录就可以查看光驱里的内容了。

**临时文件：**

- **/run**：是一个临时文件系统，存储系统启动以来的信息。当系统重启时，这个目录下的文件应该被删掉或清除。如果你的系统上有 /var/run 目录，应该让它指向 run。

- **/lost+found**：一般情况下为空的，系统非法关机后，这里就存放一些文件。

- **/tmp**：这个目录是用来存放一些临时文件的。

**账户：**

- **/root**：系统管理员的用户主目录。

- **/home**：用户的主目录，以用户的账号命名的。

- **/usr**：用户的很多应用程序和文件都放在这个目录下，类似于windows下的program files目录。

- **/usr/bin：**系统用户使用的应用程序与指令。

- **/usr/sbin：**超级用户使用的比较高级的管理程序和系统守护程序。

- **/usr/src：**内核源代码默认的放置目录。

**运行过程中要用：**

- **/var**：存放经常修改的数据，比如程序运行的日志文件（/var/log 目录下）。

- **/proc**：管理**内存空间！**虚拟的目录，是系统内存的映射，我们可以直接访问这个目录来，获取系统信息。这个目录的内容不在硬盘上而是在内存里，我们也可以直接修改里面的某些文件来做修改。

**扩展用的：**

- **/opt**：默认是空的，我们安装额外软件可以放在这个里面。

- **/srv**：存放服务启动后需要提取的数据**（不用服务器就是空）**

## VMTools

点击vm菜单中的install vmware tools

### 共享文件夹设置

虚拟机->设置->选项

共享文件夹位置mnt/hgfs

## 系统目录结构

在/home内生成用户文件夹

> useradd tom
>
> userdel -r tom

## 远程登录Linux

> setup

sshd服务是监听远程登录服务 22号端口

### 操作xshell

新建会话->输入ip->SSH用户名指linux用户名

## vi/vim

vim是vi的增强版本

### vi/vim的三种模式

- 正常模式

  以vim打开一个档案就是正常模式。在这个模式中可以使用上下左右来移动光标，可以使用删除字符或删除整行，也可以使用复制粘贴来处理你的文件数据

- 插入模式/编辑模式

  在这个模式中可以输入内容。

  按下iIoOaArR等任何一个字谜后才会进入编辑模式，一般来说按i即可

- 命令行模式

  在这个模式中可以提供相关指令，完成读取、存盘、替换、离开vim、显示行号等动作。

### 快速入门案例

> vim hello.java

i进入插入模式

esc进入命令行模式

> :wq 保存并推出
>
> :q 退出前提示
>
> :q! 强制退出不保存

![1570689102235](C:\Users\wangqi\AppData\Roaming\Typora\typora-user-images\1570689102235.png)

### 常用快捷键

![1570677347454](C:\Users\wangqi\AppData\Roaming\Typora\typora-user-images\1570677347454.png)

7)先set nu 再输入20 再shift+g

## 开机、重启和用户登录 注销

shutdown -h now 立刻关机

shutdown -h 1 1分钟后关机

shutdown -r now 现在重启计算机

halt 关机

reboot 现在重启计算机

sync 把内存同步到磁盘

**关机和重启前运行sync命令**

## 用户管理

### 添加用户

> useradd [选项] 用户名

> useradd -d 组名 用户名

> useradd nt 实际自动创建了一个名为nt的用户组

#### 实际案例

添加一个用户nt

cd 表示change directory

注意

> useradd -d /home/bej rml 

#### 指定/修改密码

> passwd 用户名

### 删除用户

userdel用户名

#### 实际案例

删除用户

> userdel

删除用户及家目录

> userdel -r

(-r指向下递归 -f指直接删除不做任何提示)

### 查询用户信息

> id 用户名

### 切换用户

> su -用户名

回到原用户

> exit

查询当前用户

> whoami

### 用户组

#### 介绍

系统可以对有共性的多个组进行统一管理

#### 命令

> groupadd 组名
>
> groupdel 组名
>
> useradd -g 用户组 用户名
>
> usermod -g 用户组 用户名

### 用户和组的相关文件

#### /etc/passwd 文件

#### /etc/shadow 文件

#### /etc/group 文件

## Linux实操篇 运行指令

### 七个运行级别

0. 关机
1. 单用户(找回丢失密码)
2. 多用户无网络服务
3. 多用户有网络服务
4. 保留
5. 图形界面
6. 重启

系统的运行级别配置文件/etc/inittab

/etc/inittab的id:5:initdefault.这一行中的数字

centos 7好像只有两种模式了

### 切换运行级别的指令

> vim /etc/inittab
>
> init 0/1/2...

### 帮助指令

> man ls
>
> help ls

### 找回root密码

思路:进入到单用户模式，修改用户密码 

原理:进入到但命令模式，用户不需要密码就可以登录

操作:在引导时敲enter  ->输入e ->选中第二行(编辑内核)输入e ->在这行输入1 ->再敲enter ->再输入b ->进入单用户模式

​	此时可以使用passwd来修改root密码

### pwd 当前位置

### ls

> ls -a 显示所有
>
> ls -l 列表显示

### cd

> cd ~或cd	回到自己的家目录
>
> cd ..	上一级目录

### mkdir

mkdir [选项] 要创建的目录

> mkdir /home/xox

mkdir /home/xox/lsn 不行，要一次性生成多级目录要

> mkdir -p /home/xox/lsn

### rmdir

rmdir [选项] 要删除的目录，但只能删除空目录

> rmdir /home/xox

要删除非空目录

> rm -rf /home/xox

### touch

创建空文件

> touch hello1.txt hello2.txt

### cp

复制文件/文件夹

> cp [选项] source dest
>
> cp ok1.txt copytest/

常用选项-r：复制整个文件夹

> cp -r copytest/ rml/
>
> \cp -r copytest/ rml/ 不提示强制覆盖

### rm

删除文件/目录

> rm 只能删除文件
>
> rm -f 强制删除文件
>
> rm -rf 删除整个目录

f指force 不提示强制执行

### mv

移动文件与目录 或重命名

> mv oldNameFile newNameFile
>
> mv /temp/moveFile /targetFolder

### cat

以只读的方式查看文件内容

> cat [选项] 要查看的文件
>
> -n 显示行号

实例

> cat -n /etc/profile | more	|more分页显示，空格翻页
>
> cat 文件A 文件B 两个同时显示

### more

基于vi编辑器的文本过滤器，以全屏分页方式显示文本文件的内容

more指令中含有快捷键

- 空格 向下翻页
- enter 向下一行
- q 离开more
- ctrl+f 向下滚动一屏
- ctrl+b 返回上一屏
- = 输出当前行的行号
- f输出文件名和当前行号

> more 文件名

### less

快速打开大文件

快捷键

- /字串 向下搜寻[字串]：n向下查找 N向上查找
- ?字串 向下搜寻[字串]：n向下查找 N向上查找

### >      >>

> \>输出重定向:会将原文件覆盖
>
> \>>追加

> ls -l >a.txt	(功能：列表内容写入a.txt中(覆盖写))
>
> ls -al>>aa.txt	(功能：列表内容追加到aa.txt末尾)
>
> cat 文件1>文件2	(功能：文件1的内容覆盖到文件2)
>
> echo "内容" >>文件

作业:将日历写入/home/cal.txt

> cal > /home/cal.txt

### echo

echo输出内容到控制台

> echo [选项] [输出内容]

案例:echo输出环境变量，输出当前环境路径

> echo $PATH

案例:echo输出hello world!

> echo hello world!

### head

head用于显示文件的开头部分，默认显示前十行

> head 文件	显示前十行
>
> head -n 5 文件	显示前5行

案例：查看/etc/profile 前5行

### tail

tail用于输出文件尾部的内容，默认显示前十行

>  tail 文件	显示后十行
>
>  tail -n 5 文件	显示后5行
>
>  tail -f 文件	实时追踪该文档所有更新

案例：实时监控mydate.txt，看看实时追加的日期

> tail -f mydate.txt

### ln

软链接,类似于快捷方式

> ln -s [原文件或目录] [软链接名]

案例:

> ln -s /root LinkToRoot

### history

> history
>
> history 10	最后10个指令
>
> !170	立即执行170号指令

### date

> date 
>
> date "+%Y-%m-%d"
>
> date "+%Y-%m-%d %H:%M:%S"

案例 设置系统时间

>date -s "2019-10-18 17:08:15"

### cal

查看日历指令

> cal [选项]

案例：显示2020日历

> cal 2020