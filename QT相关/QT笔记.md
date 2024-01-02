## 1	Pro文件解读

```
#QT工程模块变量，引入了Qt的core和gui模块
#加载模块     core核心模块     gui界面模块
QT       += core gui

#但QT版本大于4以上 就需要加上widgets模块
greaterThan(QT_MAJOR_VERSION, 4): QT += widgets


#配置QT  支持C++11标准
CONFIG += c++11

#指定目标，生成可执行文件名
TARGET =01helloWorld

#生成文件的类型
TEMPLATE = app




#使用过时的API 会报警告 与错误
# The following define makes your compiler emit warnings if you use
# any Qt feature that has been marked deprecated (the exact warnings
# depend on your compiler). Please consult the documentation of the
# deprecated API in order to know how to port your code away from it.
DEFINES += QT_DEPRECATED_WARNINGS

# You can also make your code fail to compile if it uses deprecated APIs.
# In order to do so, uncomment the following line.
# You can also select to disable deprecated APIs only up to a certain version of Qt.
#DEFINES += QT_DISABLE_DEPRECATED_BEFORE=0x060000    # disables all the APIs deprecated before Qt 6.0.0


#加载项目里面的文件

SOURCES += \
    main.cpp \
    mybntton.cpp \
    widget.cpp

HEADERS += \
    mybntton.h \
    widget.h

FORMS += \
    widget.ui


# 规则的说明  可删无大碍
# Default rules for deployment.
qnx: target.path = /tmp/$${TARGET}/bin
else: unix:!android: target.path = /opt/$${TARGET}/bin
!isEmpty(target.path): INSTALLS += target

DISTFILES += \
    readme

```





## 2	一些说明

```
/*
 * Ctrl + R   运行
 *  Ctrl + B    编译
 *  Ctrl + i  自动对齐
 *  Ctrl + Shift + 上下键     整行移动
 *  Ctrl + /   注释
 *	Ctrl + f   查找、替换
 *	Alt	+	Enter 	快速添加函数定义
 *	Ctrl + Shift + R  修改变量名并应用到所有
 *	Ctrl + Num(1-8) 快捷窗口切换
 *	
代码的书签功能：
 *	Ctrl + M	添加，删除书签
 *	Ctrl + .	移动到下一个书签的位置(这个点是小数点)
 
 *  F1   帮助文档
 *  F2或者Ctrl + 鼠标点击      标识符相关代码跳转
 *  F4    同名h ,cpp 文件之间的跳转
 *
*/



//Qt的父窗口  以左上角为0，0  坐标
//向右为X
//向下为Y

//注意：：：父对象释放的时候会自动释放子对象（通过children列表）
//子，父对象必须直接或间接继承OBject



1，信号与槽
       信号--》发生的事件
       槽（slot）--》》》响应信号的动作
       他们本质上都是函数

//把信号与槽函数关联
connect(ui->loginBt, (clicked(bool)),this,SLOT(login()));
        信号发送者   发送的信号        信号接收者， 接收后所做的事情（槽）



F1帮助文档中有标准槽，以及标准信号可供参考

信号与槽  是多对多的关系
一个信号可以接到多个槽
一个槽也可以接多个信号

信号可connect
或者disconnect

信号与槽  之间的参数类型必须一致，个数上信号的参数可以多但是不能少


```





## 3	组件添加样式以及添加资源文件

右击组件可添加样式，注意如果要添加资源的话

流程如下

1，右击项目名，点击add new,选择添加QT资源文件，命名文件名

2，点击“添加”，添加前缀，添加文件即可

特别注意：：

​	如果要添加图片作为背景，为了防止图片胡乱填充，可以在QSS语句中

加一个作用范围，列如

```
QMainWindow{     中间的QSS语句     }
```





## 4	QT中F1帮助文档的使用

1，所有U界面中的组件，在帮助文档中所有组件的相关搜索要加上Q

比如说    LineEdit---------》》》》  QLineEdit

2.一些基础的函数说明

```C++
QLineEdit::QLineEdit(QWidget *parent = nullptr)

/*
	这里的parent======》》》》输入框对象的父窗口
	父窗口就是：：组件嵌套在哪个窗口，哪个窗口就是父窗口    
*/
```



## 5	设置程序窗口的图标和名字

在QWidget 的窗口下找到  WindowsTitle  ,windowsicon修改即可







## 6	Qt主要模块----

Qt常见模块包括但不限于：

1. Qt Core：提供了Qt应用程序的核心非GUI功能，包括容器类、文件和数据处理等。
2. Qt GUI：提供了图形用户界面相关的功能，如窗口管理、事件处理、绘图等。
3. Qt Widgets：提供了各种常见的GUI组件，如按钮、标签、文本框等。
4. Qt Network：提供了网络通信功能，支持TCP/IP和UDP协议等。
5. Qt SQL：提供了数据库访问功能，支持MySQL、PostgreSQL等多种数据库。
6. Qt Multimedia：提供了音频和视频播放功能，并且能够与相机进行交互。
7. Qt WebEngine：基于Chromium引擎的Web浏览器模块，在Qt 5中作为一个单独的模块发布。
8. Qt Quick/QML：一种声明性语言，可用于快速构建动态用户界面和流畅的交互体验。它还可以与C++代码进行集成以实现高级功能。

以上是Qt常见模块之一。在学习这些模块时需要注重实践，并且根据自己的需求选择相应的模块进行深入学习。



## 7	消息对话框的使用

![image-20230525220049761](typora-user-images\image-20230525220049761.png)

其中主窗口的按键跳到槽，然后直接调用上面的静态函数，如information,按键按下时即可跳出消息框显示出来

![image-20230525220359762](typora-user-images\image-20230525220359762.png)

![image-20230525220448487](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230525220448487.png)



## 8	messageBos .exec()使用

![image-20230525221801710](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230525221801710.png)

可以用来判断messageBos 消息框的选择



## 9	Gui应用程序消息处理模型

![image-20230526123252699](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230526123252699.png)



![image-20230526123430423](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230526123430423.png)



## 10	Qstring 的使用

```C++ 
/*
QString 可以直接使用运算符  +    +=    进行字符串的拼接
*/
```

也可以使用以下函数

![image-20230526220012708](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230526220012708.png)

![image-20230526220415500](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230526220415500.png)

![image-20230526220832941](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230526220832941.png)

![image-20230526224112547](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230526224112547.png)

![image-20230526224308008](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230526224308008.png)

![image-20230527143604333](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230527143604333.png)

![image-20230527143634426](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230527143634426.png)



![image-20230527143713515](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230527143713515.png)





## 11	信号与槽的一些说明

![image-20230527145804333](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230527145804333.png)

![image-20230527150121526](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230527150121526.png)





## 12	QT工程中控件的代码说明（个人理解）

1，在代码中，类似按键的这些控件用代码实现时，先在对应的H文件的**类中进行变量的申明**

​			它们都被申明为指针变量（不给初值）

如图![image-20230527151526914](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230527151526914.png)



2，然后在CPP的类中的构造函数中，进行初始化操作（new），与此同时给定（指定）控件的标题标签，与父指针窗口

如图![image-20230527151440776](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230527151440776.png)







## 13	QT中的document（）是什么意思，怎么用？？

在Qt中，document()是QTextEdit、QTextBrowser和QPlainTextEdit等文本编辑器控件的一个公共成员函数，用于获取文本编辑器的文档对象。文档对象是一个QTextDocument类型的对象，它用于管理文本编辑器中的文本内容和格式。

使用document()函数可以获取文本编辑器的文档对象，然后可以通过文档对象来修改文本内容和格式，例如：

```cpp
// 获取文档对象
QTextDocument *doc = ui->textEdit->document();

// 在文本编辑器中插入一段文本
doc->insertPlainText("Hello World!");

// 设置文本的字体和颜色
QTextCursor cursor = ui->textEdit->textCursor();
QTextCharFormat format;
format.setFontFamily("Arial");
format.setFontPointSize(12);
format.setForeground(Qt::red);
cursor.setCharFormat(format);
```

在上面的代码中，我们首先通过document()函数获取了文本编辑器的文档对象，然后使用insertPlainText()函数在文本编辑器中插入了一段文本。接着，我们通过textCursor()函数获取了文本编辑器的光标对象，然后使用setCharFormat()函数设置了文本的字体和颜色。

总之，document()函数是Qt中处理文本编辑器控件的重要函数，它可以让我们更加灵活地管理和操作文本内容和格式。





## 14	代码实现的QT的布局

### 分裂器

![image-20230529100944749](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230529100944749.png)

![image-20230529100957860](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230529100957860.png)





第一个示例如下

![image-20230529110533656](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230529110533656.png)



在构造函数的定义中，添加下面代码

![image-20230529110709705](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230529110709705.png)

![image-20230529111042430](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230529111042430.png)

![image-20230529111111253](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230529111111253.png)



### 停靠窗口

![image-20230529111335474](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230529111335474.png)



### 排版布局

![image-20230529135846461](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230529135846461.png)

如上述所述，创建一个QGridLayout 的对象，可控制其他控件在本窗口的布局位置

其中的  1，1, 1, 2   表示这个控件占两个位置的大小











## 15	文件信息相关

### 打开文件选择对话框

![image-20230529141213275](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230529141213275.png)

```C++ 
这段代码的作用是打开一个文件选择对话框，让用户选择一个文件，并将选择的文件名显示在一个名为FileNameLineEdit的LineEdit控件中。

具体来说，代码中的QFileDialog::getOpenFileName()函数用于打开文件选择对话框，它有四个参数：

this：表示父窗口，即文件选择对话框的父窗口。

"打开"：表示文件选择对话框的标题。

"/"：表示文件选择对话框的打开路径，默认为当前路径。

"files(*)"：表示文件选择对话框的过滤器，用于指定可以选择的文件类型。

当用户选择了一个文件后，getOpenFileName()函数会返回一个QString类型的文件名，该文件名存储在strFileName变量中。然后，代码使用FileNameLineEdit->setText()函数将文件名显示在名为FileNameLineEdit的LineEdit控件中。

需要注意的是，该代码需要在一个QWidget类的成员函数中执行，因为它使用了this指针来表示父窗口。另外，需要在文件选择对话框的标题、过滤器等参数中根据实际需求进行修改。
```



### 获取文件属性

```C++
#include <QCoreApplication>
#include <QDebug>
#include <QFileInfo>

int main(int argc, char *argv[])
{
    QCoreApplication a(argc, argv);

    // 文件路径
    QString filePath = "/path/to/file.txt";

    // 创建一个QFileInfo对象
    QFileInfo fileInfo(filePath);

    // 获取文件名
    QString fileName = fileInfo.fileName();
    qDebug() << "File Name: " << fileName;

    // 获取文件路径
    QString fileDir = fileInfo.absolutePath();
    qDebug() << "File Path: " << fileDir;

    // 获取文件大小（字节数）
    qint64 fileSize = fileInfo.size();
    qDebug() << "File Size: " << fileSize << "bytes";

    // 获取最后修改时间
    QDateTime lastModified = fileInfo.lastModified();
    qDebug() << "Last Modified Time: " << lastModified.toString();

     return a.exec();
}

```







## 16 Qt中UI控件的说明

<img src="C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230529154746895.png" alt="image-20230529154746895" style="zoom: 50%;" />

<img src="C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230529154918416.png" alt="image-20230529154918416" style="zoom: 50%;" />

![image-20230529162150034](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230529162150034.png)

![image-20230529162211302](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230529162211302.png)

![image-20230529162237268](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230529162237268.png)





## 17	QT 程序打包（待解决）

我本想着一个一个程序打包没啥困难的事，可是翻阅了7，8篇帖子，都解决不了这个问题

要么是找不到DLL文件，要么是编号000007的错误（其实就还是外部库DLL不足，程序运行失败），无语了，

有博主说，要下载一个软件可以自动检索所需要的打包文件，可是链接下面的下载不了，游览器本省的问题，

还有就是修改坏境变量，可是这样自己的似乎可以跑了，但是给别人的电脑还是运行不了，

还有的说如果直接网上下载一个现成的DLL文件，没得用

啊啊啊啊啊啊啊啊啊啊

玩尼玛

Qt中在release下编译运行（不能用debug），在文件中找到此时编译好的ｅｘｅ文件，复制到一个新的文件夹中，

记录此时这个新文件夹的位置路径

然后如下

![image-20230530145350997](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230530145350997.png)

打包到这一步不一定能运行，很可能会缺少外部库文件DLL，会报错，今天先到这（2023-5-30）





## 18	音效的添加

![image-20230530150032763](C:\Users\gg\AppData\Roaming\Typora\typora-user-images\image-20230530150032763.png)

注意，要先添加资源文件（音乐文件）





## 19	QT多线程的使用说明

简单使用如下

![image-20230530155357030](typora-user-images\image-20230530155357030.png)
