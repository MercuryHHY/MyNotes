# shell脚本

## 0.shell是什么东西

```
shell是一个命令解析器
我们可以把要执行的命令，以某种语言的方式，组织起来交给shell去执行。
这种命令的组织方式就是shell脚本语言。
	.c  .cpp .bmp .mp4
	xxxx.sh是多个命令的组织文件，shell脚本文件
	是一个普通文件，以shell脚本语言的方式把多条命令组织起来的一个普通文件。

./xxx.sh把这些命令全部交给shell命令解析器去执行 

命令解析器其实就是一个程序
/bin/bash 
/bin/sh
/bin/dash
...
都是shell解析程序

shell  
shell是一个用C语言编写的程序，是用户使用Linux的桥梁。
shell是一种命令语言，又是一种程序设计语言。

shell script:shell脚本：由shell编写的脚本程序。
shell 编程指shell脚本编程，不是指开发shell本身。
```

## 1.shell脚本文件

一个简单的shell脚本文件1.sh

```sh
#!/bin/bash  
echo "hello world" #我是注释
```

改变脚本的权限chmod +x filename

运行脚本./1.sh

## 2.shell变量 

```
在shell脚本文件中，我们可以定义变量。
shell变量没有类型的概念，全部都是字符串。
shell变量也无需定义，直接用就可以了。
变量名=值
	name=vlaue
引用变量：引用变量的值
	$变量名  or 
	${变量名}
	eg:
		var=sb250
		$var ${var}
```

**shell变量有四种**

### a.自定义变量

```
如:
	var=sb250
	DATE=`date`
		``反撇号，引用里面那个命令或者程序或脚本的输出结果（标准输出，
		标准出错）
```

### b.位置变量

> 指的是传递给脚本文件或函数的参数

```
如：./test.sh 123 abc 
在shell脚本或者shell函数中
	$0 -> 第一个参数，命令行程序名 
	$1 $2 $3...$n表示第一个到第n个参数的名字
	$#表示命令行参数(不包括脚本名)的个数
	$@包含所有的命令行的参数
	$@ <==> "$1" "$2" "$3" ...
```

<img src="shell%E8%84%9A%E6%9C%AC.assets/image-20220711155358930.png" alt="image-20220711155358930" style="zoom:67%;" />

```
$*包含所有的命令行的参数
$*<==> "$1C$2C$3....$n"
C是IFS(内部域分隔符intetnal  field seprator)的一个字符 
默认是空格 Tab 换行符 IFS=" \t\n"

$?表示前一个命令或程序的退出码（返回值，进程的值）
main函数返回值或exit(值)
```

**练习**

```
时间5分钟
编写一个shell脚本。把脚本的参数的个数，以及每一个参数都打印出来。
```

### c.shell环境变量

```
环境变量：在同个终端下面所有的进程都可以共享的变量。
HOME:用户主目录的路径
PATH:命令或可执行程序的搜索路径
	你们有没有发现一个问题：
	我们在运行一个命令的时候，如“ls”
	并没有指定这个命令的路径，那么系统怎么知道这个命令或者程序文件在哪里呢？
	环境变量PATH
	PATH的值:dir1:dir2:...
```

![image-20220711161503668](shell%E8%84%9A%E6%9C%AC.assets/image-20220711161503668.png)

```
修改环境变量的值：
	export 环境变量名=新值 
	如：
		export PATH=$PATH:/home/china
	如果仅在终端修改环境变量，这个环境变量的新值只在终端有效。
	/etc/profile修改环境变量，对整个系统都有效
```

### d.shell数组

```
数组名=(vlaue1 vlaue2 vlaue3 ...)
数组名[下标]=vlaue 下标0 1 2 3 ..n-1

引用数组：引用整个数组（引用数组中所有的元素）
	${数组名[*]}
```

<img src="shell%E8%84%9A%E6%9C%AC.assets/image-20220711163537916.png" alt="image-20220711163537916" style="zoom:67%;" />

```
引用数组的下标
	${数组名[下标]}
	${数组名} 引用数组的第一个元素
```

<img src="shell%E8%84%9A%E6%9C%AC.assets/image-20220711163730780.png" alt="image-20220711163730780" style="zoom:67%;" />

## 4.shell脚本语句

### a.说明向语句（注释）

以#开头的行，就是注释

### b.功能性语句

任意的操作系统命令（如：echo ls cd date...）

shell内部命令 自编程序

```shell
#!/bin/bash 
ls 
pwd 
./a.out  #都是可以的
```

```
read:在shell中表示从终端获取输入
如：
	read var1 var2
	从终端获取两个字符串，第一个字符串保存在变量var1中第二个字符串保存在
	变量var2中
	“以空格分开”
```

```shell
#!/bin/bash
read var var1
echo $var
echo $var1
```

![image-20220711165124357](shell%E8%84%9A%E6%9C%AC.assets/image-20220711165124357.png)

![image-20220711165139323](shell%E8%84%9A%E6%9C%AC.assets/image-20220711165139323.png)

```
重定向问题：
1）输入重定向
	命令的输入请求通常是标准输入设备（如：键盘）提交请求，我们也可以很方便
	的 把输入重定向到一个文件，这种情况我们称之为输入重定向。
	在命令后添加<filename
	该命令的所有输入都来自于filenme所制定的文件
2）输出重定向
	命令的输入通常是提交到标准输出设备（如：终端），也可以很方便的转向到
	一个文件代替，这叫输出重定向。
	在命令后添加>filename
	在命令后添加>>filename
	>会先清空filename的内容（如果有），然后输出filename
	>>追加，把输出内容添加到filename指定的文件的末尾
```

![image-20220711165617055](shell%E8%84%9A%E6%9C%AC.assets/image-20220711165617055.png)

<img src="shell%E8%84%9A%E6%9C%AC.assets/image-20220711165952798.png" alt="image-20220711165952798" style="zoom:67%;" />

```
expr:算数运算命令 expr主要用于简单的整数运算 + - * / %
如：
	expr 5 + 3
	(操作数与操作符，前后至少需要一个空格)
	ret=`expr 5 + 3`
```

```shell
#!/bin/bash
ret=`expr 5 % 3`
echo $ret
```

**练习一**

```
写一个脚本计算两个整数的和，两个整数通过参数传入
./1.sh 3 4
```

```shell
#!/bin/bash
ret=`expr $1 + $2`
echo $ret
```

```
test:
	test语句可以测试三种对象
	字符串 整数 文件
	test 测试成功 返回0
		 测试不成功  返回1
a.字符串测试
	=测试两个字符串的内容是否完全一致 
	test "abc" = "abc"
	echo $? 
	
	!=测试两个字符串内容是否不相同
	test "abc" != "abcd"
	echo $?
	
	-z zero 测试字符串是否为空
	test -z ""
	echo $?
	
	-n  not null测试字符串是否不为空
	test -n "abc"
	echo $?
	
	eg:
	str=
	test -n $str
	echo $?
	本来应该返回1的，但是返回0 
	
	在测试字符串的时候，需要防止字符串为空
	“技巧”：引用字符串变量的时候，后面额外加一个字符${var}x
	如：
		判断变量${var}和变量${var1}是否相等
		test ${var}x = ${var1}x
```

**练习二**

> 在键盘上输入一个字符串(read)，测试输入的字符串是否等于“good”

```shell
#!/bin/bash
read var
test ${var}x = "goodx"
echo $?
```

<img src="shell%E8%84%9A%E6%9C%AC.assets/image-20220712092933496.png" alt="image-20220712092933496" style="zoom:67%;" />

```
b.整数测试
	a -eq b equal测试两个整数是否是相等的   ==
		test 3 -eq 4
		test $i -eq 4
	a -ne b not equal测试两个整数是否不相等 !=
    a -gt b greater than >
    a -ge b greater equal >=
    a -lt b litter than <
    a -le b litter equal <=
```

```shell
#!/bin/bash
test $1 -eq $2
echo $?
```

```
c.文件测试 
	-d filename 测试filename是否为目录(directory)
	-f filename 测试filename是否为普通文件(file)
	-l filename 测试filename是否为链接文件(link)
	-r filename 测试filename是否为存在并且可读(read)
	-w filename 测试filename是否为存在并且可写(write)
	-x filename 测试filename是否为存在并且可执行(execute)
	-s filename 测试filename是否为存在并且长度不为0(size)
	
	f1 -nt f2 测试f1是否比f2更新  nt newer than 
	f1 -ot f2 测试f1是否比f2更旧  ot older than
	最后，test命令可以用[]来简写
	test expression <==> [ expression ]
	如：
		test ${var1} = ${var2}
		<==>
		[ ${var1} = ${var2} ]
	
    test的复合表达式
    	组合两个或两个以上的表达式称为复合表达式，为了使用复合表达式，你可
    	以用test([])内置的操作符，也可以用条件操作符：
    1.使用test内置的操作符来创建复合表达式
    	test expr1 "test_builtin" expr2
    	test_builtin:test内置的操作符
    		-a  and  并且
    		-o  or   或者
    	eg:
    		一个文件($1)是否为普通文件，而且这个文件1比文件2($2)更新 
    	test -f $1 -a $1 -nt $2
    	5>4>3
    	test 5 -gt 4 -a 4 -gt 3
    2.使用条件操作符(&& || !)来创建复合表达式
    	test expr "op" expr2
    	"op" && || !
    	eg:
    		test 5 -gt 4 && 4 -gt 3
    		[ 5 -gt 4 ] && [ 4 -gt 3 ]
```

### c.结构性语句

> 分支和循环语句

#### c1.分支语句

```
if command;then
	....
	语句列表 
else #else不要
	...
	语句列表
fi
例子：
	if [ ${var}x = "goodx" ];then
		echo "good"
	else 
		echo "not good"
	fi
```

**练习三**

> 从键盘上输入一个整数，判断这个整数是否为奇数

```shell
#!/bin/bash
read var
ret=`expr $var % 2`
if [ $ret -eq 1 ];then
	echo "yes"
else 
	echo "no"
fi
```

#### c2.多路分支语句

```
case 字符型变量 in
	模式1)
		...
		;;#类似于C语言中的break，但是在shell里面;;一定要
	模式2)
		...
		;;
	...
	模式n)
		...
		;;
esac
case语句真正强大的地方在于它可以使用模式而不是固定的字符来匹配。一个模式是由
正规字符和特殊通配符组成的字符串，该模式可以用正则表达式(*请见正则表达式知识
点)(有限支持，不能"|")
	* shell通配符 代表任意多个（也可以是0个）字符
	? shell通配符 代表一个任意字符 
	例子：
		filename=$1
		case $filename in 
			*.c) #匹配所有以.c结尾的文件名
				echo "c source file"
				;;
			*.h)
				ehco "header file"
				;;
			*.cpp)
				ehco "c++ source file"
				;;
		esac
```

#### c3.循环语句

```
for 变量名 in 单词表 
do
	...循环体语句 
done
"单词表”:以空白符分隔开来的字符串列表 
如:a ab c ddd 
for执行的次数就是“单词表”中的单词的个数，并且每次执行的时候，“变量”的值就
取下一个单词的值
如：
	for i in a b c ddd
	do 
		echo $i
	done 
	===>
		a
		b
		c
		ddd
for可以写成于C风格类型的循环
sum=0
for ((i=1;i<100;i=i+2))
do
	sum=`expr $sum + $i`
done 

echo "sum=$sum"
```

**练习四**

> 用shell求出100以内所有3的倍数之和

```shell
sum=0
for ((i=3;i<100;i=i+3))
do
	sum=`expr $sum + $i`
done 

echo "sum=$sum"
```

```
while 语法
while 命令或表达式
do 
	...
done 
如：
	求一个普通文件有多少航 
	line=0
	while read var  #读取文件的一行 
	do
		line=`expr $line + 1`
	done<"$1"    #./1.sh 1.txt 输入重定向
	echo "there are $line lines in $1"

while也可以写成C风格类型
sum=0
i=1
while ((i<=10))
do
	sum=`expr $sum + $i`
	i=`expr $i + 1`
done
```

**练习五**

> 用while求1-100所有奇数的和

```shell
#!/bin/bash
sum=0
i=1
while ((i<=100))
do
	sum=`expr $sum + $i`
	i=`expr $i + 2`
done
```

```
until
语法如下：
until 命令或表达式
do
	...
done
until和while的功能相似的，所不同的是until只当测试的命令或表达式的值为假
的时候才执行循环体的命令列表，条件成立，则退出循环，这一点和while相反
eg
sum=0
i=1
until ((i>100))
do
	sum=`expr $sum + $i`
	i=`expr $i + 1`
done 
```

**练习六**

> 使用until求1-100所有的3的倍数的和

```
break和continue
	break n
		跳出第n层循环 
	continue n
		转到最低的第n层循环语句执行下一次循环
		数字n表示，第几层循环
	break和continue后面不加n
	和c语言中的含义一样的
```

## 5.shell函数

```
function_name()
{
	...
}
function_name:你自己定义的函数名，名字的取法和C语言类似
函数调用：
	function_name arg1 arg2 agr3 ...
	在函数内部
		arg1 --- $1
		arg2 --- $2
		arg3 --- $3
		...

取得函数返回值：通常有两种方式
1)ret=`function_name arg1 arg2 ...`
``执行函数function_name的时候的标准输出的内容
eg:
sum()
{
	a=$1
	b=$2
	s=`expr $a + $b`
	echo $s #return s;
}
r=`sum 3 4`
2)function_name arg1 arg2 ...
	ret=$?
	$?永远表示最近一条命令或者一个程序的退出码（main返回值/exit(n)）
	eg:
	sum()
	{
		a=$1
        b=$2
        s=`expr $a + $b`
        return $s 
	}
	r=`sum 3 4`
	echo $?
```

**作业**

> 写一个shell脚本，打印1000以内所有的质数