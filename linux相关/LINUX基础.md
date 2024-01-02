# LINUX基础

## 1.LINUX基础命令

### a.APT

> advanced packing tool

​	**ubuntu中功能最强大的命令行软件包管理工具，用于获取、安装、编译、卸载和查询软件包，以及检测软件信号关系。**

工具原理

`/etc/apt/source.list`

<u>用来执行UBUNTU的软件源服务器的地址的。</u>

修改源

查改你ubutnu对应版本的软件源服务其的地址列表

然后把`/etc/apt/source.list`的内容替换

举个栗子

```
1.输入命令修改source.list文件。加sudo(超级管理员)
	sudo gedit /etc/apt/source.list
2.修改源
3.修改完成后，保存文件，警告不管，运行下面的命令
	sudo apt-get update
```

几个常用的命令

`sudo apt-get update`

下载更新软件包列表的信息

如果只指定软件源的地址，那我怎么知道，服务器上有哪些软件呢？可以通过apt-get update这个命令把服务器上面最新的软件包列表信息下载到本地。

**sudo apt-get install 要安装的软件包的名字**

**sudo apt-get remove 要删除的软件包的命令** 

**sudo apt-cache search 根据正则表达式检索软件包**

如：

​	sudo apt-cache search game

**练习一：使用apt-get来安装某个软件**

### b.vi/vim

​	vi/vim是linux中最基本，最常用，功能最强大的**命令行编辑器**。vim是vi的升级版本。

#### 工作模式

```
命令模式
	键盘上所有的输入字符都当做是一个命令 
输入模式(insert)
	键盘上所有的输入字符都当做是文本 
```

#### 模式切换

```
命令模式--->输入模式
	i/I:insert 
		i:进入输入模式后，光标不动
		I:进入输入模式后，光标会移动到行首
	a/A:append 
		a:进入输入模式后，光标往后移动一个字符
		A:进入输入模式后，光标移动到行末  
	o/O:open(开路）
		进入输入模式后，会新开一行
		o:在光标的下面，开一行
		O:在光标的上面，开一行 
	输入模式---->命令模式
	ESC 
```

#### 退出命令

```
:q quit未保存退出（文件的内容没有被修改）
:q! 强制退出（未保存）

:w write保存文件（但不退出）
:w filename 
	把内容保存到“filename”指定文件中“另存为”
	
:wq  保存退出 
:x  <===> :wq 保存并退出
```

#### 删除与修改命令

```
x:删除光标所在的字符
dd:delete
	刪除所在的行
ndd:
	n代表数字，删除光标及以下的行
	dd和ndd是剪切
r 
	repalce 
	替换光标所在的字符
	r加上替换的单个字符    
R 
	Repalce
	替换光标及后面的多个字符，到底是多少个字符呢？
	看你的心情（按ESC键退出）
```

#### 拷贝和粘贴

```
理解剪切板 
dd和ndd是剪切
yy
	yield
	将当前行的内容拷贝的剪切板上去
	nyy
p 
	print
	将剪切板上的内容粘贴到当前行的后面
P
	Print
	将剪切板上的内容粘贴到当前行的前面
```

#### 撤销命令

```
u/U
undo撤销
```

#### 搜索命令

```
/要搜索的内容
n
	next  
	找下一个匹配的内容
N
	Next
	找上一个匹配的内容
```

#### 替换命令

```
s substitude替换 
:{作用范围}s/{目标}/{替换的内容}/{替换的标志}
	作用范围
	当前行：作用范围不写就表示是当前行替换
	全文：%
	选区:
		5,12 5-12行  
		.,+2 当前行及接下来的两行
	替换标志
		g global 全局替换（所有出现的目标都替换）
		i ignore 忽略大小写
```

#### 显示行号

```
:set nu
:set nonu
```

#### vi/vim配置文件

```
.vimrc
~/.vimrc
我们可以根据自己喜好去修改vim的配置
```

#### 练习：

```c
1.请同学们使用vim写一个程序，验证一下20000000以内所有的哥德巴赫猜想
	a.每个大于2的偶数都是两个素数之和
	b.每个大于5的奇数都是三个素数之和
int Is_prime(int num)
{
	if(num == 0 || num == 1) return 0;
	int i;
	for(i=2;i<=num/2;i++)
	{
		if(num%i == 0)
		{
			return 0;
		}
	}
	return 1;
}
/*
	成立1 不成立0 
*/
int Gedebahe(int num)
{
	int i;
	for(i=4;i<=num;i++)
	{
		if(i%2==0)
		{
			int a=2;
			for(;a<=i/2;a++)// a i-a
            {
            	if(Is_prime(a)&&Is_prime(i-a))
            	{
            		printf("%d =%d+%d ",i,a,i-a);
            		break;
            	}
            }
            if(a > i/2)
            {
            	return 0;
            }
		}
		else
		{
			
		}
	}
	return 1;
}

2.求二维数组的元素和的函数sum_array()
int sum_array(int a[][N],int n)//(int (*a)[N],int n)
{
	int i,j,sum=0;
    for(i=0;i<n;i++)
    {
        for(j=0;j<N;j++)
        {
            sum+=a[i][j];
        }
    }
    return sum;
}
```

### c.文件系统相关的命令

**文件系统是什么？**

​	是用来管理文件的一套组织方法以及软件系统。

**文件的组成部分**

```
文件属性 --> inode 
	文件名，文件类型，文件大小...
	inode是唯一标识文件存在与否的东西
文件内容
```

LINUX**文件系统属性结构**

```
LINUX下面文件组织方式是以“根目录/”开始的，“根目录”下面可以是目录，也可以有
文件，目录下面也可以由目录有文件。。。以这种树的形式组织起来的，树形结构。
```

<img src="LINUX%E5%9F%BA%E7%A1%80.assets/image-20220708160643045.png" alt="image-20220708160643045" style="zoom:50%;" />

**绝对路径**

以“根目录/”开始的路径

**相对路径**

不以“根目录/”开始的路径，而是以当前路径开始的路径称之为相对路径。相对路径隐藏了绝对路径。

**.和..**

.当前目录

..上一级目录

**pwd**

把当前目录的绝对路径显示出来

<img src="LINUX%E5%9F%BA%E7%A1%80.assets/image-20220708160914722.png" alt="image-20220708160914722" style="zoom:67%;" />

**cd**

```
change directory
语法：
	cd 要切换的目录（路径） 可以是相对路径也可以是绝对路径
	cd 后什么都不接
		切换到用户的主目录（家目录）下面去
	cd - 切换到刚刚来的目录
```

**ls**

```
list 列举
ls用来列举一个目录下面所有的文件（包括目录）名 
语法
 	ls [OPTION]... [FILE]...
	-a, --all 列举所有的文件信息 包括隐藏文件
       do not ignore entries starting with .
 	-l     use a long listing format
	列举出文件的详细信息
	如果省略文件或目录，则列举当前目录下面所有的文件信息
```

![image-20220708161507661](LINUX%E5%9F%BA%E7%A1%80.assets/image-20220708161507661.png)

```
在linux下，系统会为每一个用户，创建一个主目录，我们称之为用户的家目录（home
目录），一般来说，你在家里，拥来一切权限。so,一个用户在自己的Home目录用来
权限进行删除、修改等等。
linux系统一般为每一个正常登陆的用户，在/home下面创建一个以用户名命名的家
目录。
eg:/home/china
```

**mkdir**

```
NAME
       mkdir - make directories 创建一个空目录

SYNOPSIS
       mkdir [OPTION]... DIRECTORY...

-p, --parents
              no error if existing, make parent directories 
              as needed
如果要创建的目录的上面某一级或多级目录不存在则一并创建
```

**rmdir**

```
删除空目录
```

**rm**

```
删除文件或目录
NAME
       rm - remove files or directories
SYNOPSIS
       rm [OPTION]... [FILE]...
	 -f, --force 强制
              ignore nonexistent files and arguments, 
              never prompt
	非交互模式删除，不询问用户是否删除
	-r, -R, --recursive 递归
              remove directories and their contents recursively
	eg:
		rm -rf dir
```

**cp**

```
NAME
       cp - copy files and directories

SYNOPSIS
       cp [OPTION]... [-T] SOURCE DEST
       cp [OPTION]... SOURCE... DIRECTORY
       cp [OPTION]... -t DIRECTORY SOURCE...
	SOURCE 源文件
	DEST 目标 可以是文件也可以是目录 
	cp -r dir1 dir2 
	把目录dir1整体拷贝目录dir2下面去
	cp file1 file2 
	把文件file1拷贝到file2中去，把file1的内容替换file2里面的内容，如果
	file2不存在则创建
	cp file1 dir1 
	把文件拷贝到目录dir1下面去
	cp dir1 file1 不行 
[OPTION]
	-r -R 递归 当拷贝的是目录 需要用-r
	-f 非交互式
```

**mv**

```
NAME
       mv - move (rename) files
SYNOPSIS
       mv [OPTION]... [-T] SOURCE DEST
       mv [OPTION]... SOURCE... DIRECTORY
       mv [OPTION]... -t DIRECTORY SOURCE...
	mv file1 dir1
		把文件file1移动到目录dir1下面去
	mv dir1 dir2
		dir2存在
			把目录dir1整体移动到目录dir2下面去
		dir2不存在
			把目录dir1重命名为dir2
	mv file1 file2
		把file1的内容，移动到file2去
		如果file2存在，则改名
```

**cat**

```
NAME
       cat - concatenate files and print on the standard output
	在终端查看文件的内容
SYNOPSIS
       cat [OPTION]... [FILE]...
```

**touch**

```
NAME
       touch - change file timestamps(时间戳）
SYNOPSIS
       touch [OPTION]... FILE...
DESCRIPTION
       Update the access and modification times of each 
       FILE to the current time.

       A FILE argument that does not exist is created empty, 
       unless -c or -h is supplied.
       文件不存在则会创建一个空文件
       eg:
       touch 1.c 创建一个空文件1.c 
```

**file**

```
NAME
     file — determine file type 判断文件类型
```

![image-20220708163846180](LINUX%E5%9F%BA%E7%A1%80.assets/image-20220708163846180.png)

**chmod**

```
改变文件的权限位
文件权限对某个用户或组用户或其他用户而言
r read
w write
x excute
每个文件都会针对三组不同用户
user:文件所有者用户
group:文件所有者所在的组的用户 组用户 
other:其他用户
描述一个文件:ls -l 
-rwxrwxrwx 
- 普通文件
user group other
关于chmod 改变权限(mode)的方式请见第二阶段文件IO 
eg:
	chmod +x file1 为文件添加一个可执行权限（所有用户）
	chmod 0776 file1 8进制的方式改变
	111 111 110 
	rwx rwx rw-
```

![image-20220708164152470](LINUX%E5%9F%BA%E7%A1%80.assets/image-20220708164152470.png)

**==文件压缩和归档==**

```
归档文件：将一个文件或目录保存在一个文件中。“打包”
压缩文件：将一组文件或目录压缩在一个文件中。
tar 
	语法：
		tar [opition] tarfile filelist
					压缩后的文件名 需要压缩的文件列表
		opition
		-x extract 释放一个归档文件
		—c create 创建一个归档文件
		-v view 显示归档或释放过程信息 
		-f file指定归档文件的名字 
		-j 由tar生成归档文件，用bzip2压缩
		-z 由tar生成归档文件，用gzip压缩
		-u -update 仅追加比归档文件中更新的文件 

压缩
	tar -zcvf xxx.tar.gz(xxx.tagz) filelist 
	把filelist指定的文件列表用(-z gzip)gzip来压缩 
	生成一个压缩文件名为xxx.tar.gz(xxx.tagz) 
	
	tar -jcvf xxx.tar.bz2 filelist
	把filelist指定的文件列表用(-j bzip2)bzip2来压缩 
	生成一个压缩文件名为xxx.tar.bz2 
释放
	tar -xvf xxx.tar.gz(xxx.tar.bz2 ){-C 目录}
	-C 表示把解压后的文件列表，解压到指定的“目录”中
	（如果该目录不存，则报错）
```

![image-20220708165926319](LINUX%E5%9F%BA%E7%A1%80.assets/image-20220708165926319.png)

![image-20220708170002572](LINUX%E5%9F%BA%E7%A1%80.assets/image-20220708170002572.png)

![image-20220708170235137](LINUX%E5%9F%BA%E7%A1%80.assets/image-20220708170235137.png)

#### 练习

```
把你的AVL树的.c文件压缩到一个文件中
然后解压到图的code文件中
```

**链接**

```
文件
	文件属性--->inode 唯一标识一个文件存在与否 
	文件内容  
```

**硬链接**

```
ln target link_name
为文件target创建一个硬链接(link_name)
硬链接实际为文件target创建了一个新的inode
```

![image-20220711141033425](LINUX%E5%9F%BA%E7%A1%80.assets/image-20220711141033425.png)

**软链接**

```
符号链接 software
ln -s target link_name 
	为文件target创建一个软链接（优点像windowns的快捷方式）
	软链接实际上并没有为targrt创建一个新的inode
	软链接指向目标文件，软链接本身保存是目标文件的路径名
```

![image-20220711141359877](LINUX%E5%9F%BA%E7%A1%80.assets/image-20220711141359877.png)

<img src="LINUX%E5%9F%BA%E7%A1%80.assets/image-20220711141452469.png" alt="image-20220711141452469" style="zoom:67%;" />

---

如果判定两个文件的内容是否是一致的？

​	通常的做法：把两个文件的内容一一对比。这种方法不科学。

​	“文件的DNA”：DNA是文件的内容的ID，如果两个文件的DNA一致，则说明这两个文件的内容是一致的。

​	那么文件的DNA怎么获取或计算呢？

​	各家有各家的算法：

​	如：md5sum计算一个文件的MD5值，如果两个文件的MD5sum是一致的，认为这两个文件的内容是一样的。

### d.基本的系统名

**man**

```
manual手册/文档/使用说明 
	linux会为每个命令或系统函数或库函数，写一个文档（帮助文件，手册，
	使用说明）
	不同的文档，有不同的分类
	1
	2
	3
	..
	而且有时候，有同名的函数或命令 
	man用来查询一个指定的命令的相关手册（说明文档）
	语法：
		man -f 名字 
			把“名字”相关的手册分类的信息列举出来  
		man 手册页 名字 
			把相应的“手册页”关于“名字”的文档调出来
			如果省略“手册页”系统会：
			先从分类1去查找“名字”的文档，如果找到，就调出来，如果找不到则
			再从分类2去查找“名字”的文档，如果找到，就调出来，如果找不到则
			...
```

 **shutdown**

```
关机的命令
```

**reboot**

```
系统软复位，重启
```

**sudo**

```
sudo -> super do 
用超级管理员用户去执行这个命令 
```

**su name**

```
切换到Username执行的用户
root 用户 
	root用户在Linux、UNIX中拥有至高无上的权限的用户
	“超级管理员”
	
	ubuntu装机的时候，一般只会让你设置一个管理员的用户 
	如：
		china 
		当你以管理员的身份进入系统后，第一个切换到root用户 sudo -s 
```

**password [username]**

```
为用户username设置一个新密码
如果Username省略，则为当前用户设置密码 
```

### e.用户管理 

```
/etc/passwd
	用来保存用户的信息的	
```

<img src="LINUX%E5%9F%BA%E7%A1%80.assets/image-20220711143117284.png" alt="image-20220711143117284" style="zoom:67%;" />

```
用户名：口令：用于的ID(UID)：组ID(gid)：用户主目录(home):用户shell
/dec/group
	用户组的信息 
	组名：口令：组ID：成员列表
```

<img src="LINUX%E5%9F%BA%E7%A1%80.assets/image-20220711143404641.png" alt="image-20220711143404641" style="zoom:67%;" />

```
adduser username
passwd username
userdel username 

groupadd groupname
groupdel groupname
```

### f.进程管理 

```
ps
	process status
	列出系统中进程的信息
```

<img src="LINUX%E5%9F%BA%E7%A1%80.assets/image-20220711144001248.png" alt="image-20220711144001248" style="zoom:67%;" />

```
-e every 
-f full
```

![image-20220711144101550](LINUX%E5%9F%BA%E7%A1%80.assets/image-20220711144101550.png)

```
kill 
	发送一个信号给一个进程 
	eg:
		kill -9 pid
		强制终止进程(pid进程号）
```

```
top 
	动态显示或列出占用系统资源最多的进程
```

<img src="LINUX%E5%9F%BA%E7%A1%80.assets/image-20220711144612838.png" alt="image-20220711144612838" style="zoom:67%;" />

#### 练习

```
使用man查看shutdown的用法，然后运行“定时关机”的命令 

添加一个以你的命令命名的用户并切换到该用户
```

