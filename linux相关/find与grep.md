# **`find与grep`**

## 1.`find`

```
NAME
       find - search for files in a directory hierarchy
		在一个文件系统中查找一个文件
SYNOPSIS
       find   [-H]  [-L]  [-P]  [-D  debugopts]  [-Olevel] 
       [starting-point...]
       [expression]
usage
	find [path..] [opition]
	opition:
	-name pattern
    指定要查找的文件的名字，可以用通配符 
    *代表0个或者多个任意字符
    ?代表任意的一个字符
	如：
		find ./ -name *.c 
		在当前的目录(目录下面的目录...)查找以.c结尾的文件
		
	-regex pattern
	以正则表达式的方式去查找相关的文件
	如：
	find ./ -regex ".*c"
	
	-type  b|c|d|p|f|l|s指定要搜索文件的类型
    File is of type c:
    b      block (buffered) special 块设备 
    c      character (unbuffered) special 字符设备
    d      directory 目录
    p      named pipe (FIFO) 管道
    f      regular file 普通文件
    l      symbolic  link; this is never true if the -L option 
    or the -follow option is in effect, unless the symbolic  
    link  is broken.   If you want to search for symbolic 
    links when -Lis in effect, use -xtype.
			链接文件
	s      socket 套接字
	
	 -size n[cwbkMG]
     File uses n units of space, rounding up.  The following suffixes can be used:

`b'    for 512-byte blocks (this is the default if no suffix is used)
		
`c'    for bytes 字节

`w'    for two-byte words 字（根机器字长）

`k'    for Kibibytes (KiB, units of 1024 bytes) kB = 1024字节

`M'    for Mebibytes (MiB, units of 1024 * 1024 = 1048576 bytes)

`G'    for Gibibytes (GiB, units of 1024 * 1024 * 1024 = 1073741824 bytes)

	-perm mode 要查找文件的权限
	permission 权限
		mode有两种写法
		-mode 要求所有的(为1)权限位都要匹配
		如:
		-perm -664  //110110100
		/mode 要求只需要匹配一位
		如：
		-perm /664
		待查找的文件权限只要有一个匹配位就行了 
		
	-newer file
		查找比file更新的文件
		带查找的文件修改时间在file这个文件的后面即可
		
	-delete
		找到即删除 
	
	-exec command {} \;
		每找到一个文件就执行command命令
		{}代表找到的文件名。每找到一个文件就执行一次command这个命令；
		如：
		find -name ".*\.c" -exec ls -l {} \;
	
	-exec command {} +
		所有的文件查找完后，再执行command命令
		{} +代表所有查找到的文件的文件名（以空格隔开）
```

**练习**

> 把你所写 的所有的.h .c文件打包(使用find tar命令)

```
提示:
	查找.h  .c  ".*\.[ch]"
	打包 -exec tar zcvf C.tar.gz {} +
	
find /mnt/hgfs -regex ".*\.[ch]" -exec tar zcvf C.tar.gz {} +
```

## 2.`grep`

```
grep(egrep)用来在一个文本文件(ascii)中查找一个特定的字符串
	egrep是扩展的正则表达式去查找

语法：
	grep opitions [正则表达式] files 
	
	在file列出的所有的文件里面，查找以“正则表达式”所描述的字符串
	opitions 
		-n  显示查找的字符串的所有的行号
		-E  用拓展的正则表达式
			grep -E <==> egrep
		-i  ignore在字符串查找时忽略大小写  
			-i "main" <==>[mM][aA][iI][nN]
		-#  表示同时显示匹配行的上下#行 
		-c count打印每个文件匹配的个数
		-H 显示文件名
		-h 不显示文件的名字
		
		匹配内容颜色高亮显示
		--color=always 总是显示显示
		--color=never 不高亮显示
		--color=auto 自动
```

<img src="find%E4%B8%8Egrep.assets/image-20220712164333258.png" alt="image-20220712164333258" style="zoom:67%;" />