## 命名空间的说明

在C#中，使用同一个命名空间，可以达到与头文件相同的效果

在主函数的.cs 文件中自定义一个命名空间的名字，在其他.cs文件中再次使用这个命名空间，

如此，这些代码存在一个命名空间中，就相当于包含头文件的使用类似



在.net 的底层中，有很多个已经封装好的模块，每一个模块可以包含若干个命名空间，在类中想使用哪些内容，

必须引入相应的命名空间，类存在于命名空间中。



注意：：在启动cs文件中的自定义命名空间名称 ，默认与工程名一致





## internal说明（限定当前程序集）

与之相对的是publlic声明

在C#中，"internal"是一种访问修饰符，用于**控制类、方法、属性或字段**的访问级别。它的作用是限制对其修饰的成员的访问范围，使其只能在当前程序集内部访问（**何谓当前程序集**）。

具体来说，"internal"关键字表示修饰的成员只能在同一程序集中访问，而不能被其他程序集访问。这意味着，如果一个类或成员被声明为"internal"，则只能在同一个项目或程序集中使用，而不能从其他项目或程序集中访问。

"internal"修饰符对于隐藏或封装一些实现细节并将其限制在程序集内部非常有用。它提供了一种方法来控制代码的可见性，从而增加了代码的安全性和可维护性。

何谓当前程序集？？？？？？

比如说，一个类被声明为internal，那么该命名空间就是他的当前程序集，其他命名空间无法访问该类

比如说，一个函数被声明为internal，那么该类之下就是他的当前程序集，其他类无法访问该函数

注意一个问题：：

如果一个被声明为internal的类（A），将它作为另一个类（B）的泛型容器类型的属性(V)，比如 List<A> V

那么注意要将V与A的访问级别保持一致，要么都是internal，要么都是public，看工程需要而定







## 一个项目中工程结构说明



### 1，Properties文件夹（属性文件夹）

Properties文件夹下的CS文件是程序集，里面的配置信息主要是用来保存项目的版权信息

还有一些其他文件是用来保存工程中用到的资源文件的信息



### 2，Program.cs文件说明

Program.cs文件是项目的启动入口文件



### 3，引用说明

引用：：这个当前项目所需要的.net 底层模块（联想qt），添加相关引用之后，就可以使用命名空间的代码

​		它底层的的模块代码是已经封装好了的

注意：：如果项目开发中它没有自动引入底层模块，则需手动添加（右键点击引用即可）

当然，可以自己封装一个库（用dotnet支持的语言都可），然后添加引用到开发项目中

### 4，App.config文件

config文件是用来保存工程所需要的相关信息，列如 字符编码格式，所用到的模块及其版本等等

它不能重复添加，名称也不能修改，

且该文件不能只能放置在默认的根目录下，不可更改 该文件的路径





注意：： 如果在CS代码中要用到config   文件中的代码，要在引用中手动添加

![微信截图_20230703183029](picture\微信截图_20230703183029.png)





#### C# 的App.config 文件中的XML节点怎么写

在C#的App.config文件中，XML节点的写法如下：

```xml
<configuration>
  <node1 attribute1="value1" attribute2="value2">
    <node2>Node2 Value</node2>
    <node3>Node3 Value</node3>
  </node1>
  <node4>
    <subnode1>Subnode1 Value</subnode1>
    <subnode2>Subnode2 Value</subnode2>
  </node4>
</configuration>
```

在上面的示例中，`<configuration>`是根节点，`<node1>`是根节点的子节点。`<node1>`节点有两个属性`attribute1`和`attribute2`，以及两个子节点`<node2>`和`<node3>`。

同样地，`<node4>`是根节点的另一个子节点，它有两个子节点`<subnode1>`和`<subnode2>`。

您可以根据您的需求和数据结构来编写App.config文件中的XML节点。请注意，App.config文件是用于配置应用程序的文件，所以节点的结构和内容应该符合应用程序的配置需求。

注意 **此处的代码对空格符敏感**



#### C#中App.config 文件中的代码详情

这段XML代码是一个典型的C#应用程序的App.config文件的示例。它用于指定应用程序所需的支持的.NET Framework运行时版本。

让我们逐个解释这个XML结构：

- 第一行`<?xml version="1.0" encoding="utf-8" ?>`是XML声明，它指定文件中使用的XML版本和编码。

- 根元素`<configuration>`包含了应用程序的所有配置设置。

- 在`<configuration>`元素内部，`<startup>`元素用于配置应用程序的启动行为。

- 在`<startup>`元素内部，`<supportedRuntime>`元素用于定义应用程序所支持的运行时版本。它有两个属性：`version`和`sku`。

- `version`属性指定应用程序支持的.NET Framework版本，这里是版本4.0。

- `sku`属性用于指定有关所支持的.NET Framework版本的附加详细信息。在这个示例中，它表示应用程序支持".NETFramework" SKU，并且最低版本是4.7.2。

总的来说，这个配置确保应用程序在指定的.NET Framework版本和SKU下启动。

请注意，App.config 文件可以包含各种其他配置设置和部分，具体取决于您的应用程序的特定需求。



#### C#中，怎么访问App.config 文件中节点，请生成相关代码

在C#中，可以使用`ConfigurationManager`类来访问和读取App.config文件中的节点。以下是一个示例代码：

```csharp
using System;
using System.Configuration;

class Program
{
    static void Main()
    {
        // 读取App.config文件中的节点值
        string settingValue = ConfigurationManager.AppSettings["SettingKey"];

        // 输出节点值
        Console.WriteLine("Setting Value: " + settingValue);

        // 等待用户输入
        Console.ReadLine();
    }
}
```

在上面的示例中，`ConfigurationManager.AppSettings`属性用于访问App.config文件中的`appSettings`节点。其中，`"SettingKey"`是要读取的节点的键。

请确保在项目中引用了`System.Configuration`命名空间，以便使用`ConfigurationManager`类。

您可以根据自己的App.config文件的结构和需求，修改上述代码以读取和访问其他节点。







### 5，窗口文档

整个窗口设计的文件初看会有些奇怪，

首先一个窗口的设计界面   .cs[设计]

一个设计窗口的背后逻辑代码文件   .cs    注意，要右键才可进入此.cs文件

一个Design.cs 文件用来保存生成的控件代码以及相关信息的保存 ，通常此代码不用更改理会，所以才单独放置在一个单独的文件中



### 6， partial 的说明

为了工程上的便捷，使用partial声明一个类的两个部分，使其可以放置在两个不同的文件中，

当编译时，再将其两个部分合并，成为一个完整的类 ，妙哉妙哉



### 7，小细节

可以重命名.cs文件名，文件中的名字会跟着一起变

可以添加一个文件夹，将自定义的类加入文件夹中，项目不会乱，可方便类代码的管理



## 一些快捷说明

1，F1键 可以跳转到浏览器去找到关键字的相关说明

2，在一个函数的定义上一行，接续3个///   可以快捷的给函数注释（也叫文档注释）

3，输入CW，然后连续两个Tab键，就可快捷输入Console.WriteLine()

4，Ctrl+Enter   光标不动，代码下移动，留出空行

5，输入prop+连续两个Tab键，就可快捷输入属性的声明

6，pro+连续两个Tab键      public 

7, 	ctor   + 	连续两个Tab键       直接生成构造函数

8，	propfull  + 连续两个Tab键     就可快捷输入属性以及字段的声明

9,	F4   属性窗口





- if 语句：输入 “if” 后按下 Tab 键两次，会自动生成 `if(condition) { }` 的代码结构，使你只需要填写条件和代码块。
- for 循环：输入 “for” 后按下 Tab 键两次，会自动生成 `for (int i = 0; i < length; i++) { }` 的代码结构，使你只需要填写循环条件和代码块。
- 类的构造函数：输入 “ctor” 后按下 Tab 键，会自动生成类的默认构造函数。

1. 快速注释和取消注释：可以使用快捷键 Ctrl + K, Ctrl + C （注释选定的代码）和 Ctrl + K, Ctrl + U （取消注释选定的代码）。
2. 代码块收缩与展开：使用 Ctrl + M, Ctrl + M 快捷键可以实现收缩和展开代码块。
3. 代码格式化：使用快捷键 Ctrl + K, Ctrl + D 可以快速对选定的代码进行格式化，使其符合指定的代码风格。
4. 代码自动完成：在输入代码时，可以使用Tab键来自动完成已输入的代码，或者使用Ctrl + Space键调出智能提示列表，并使用上下箭头键选择正确的选项。
5. 代码导航：使用快捷键 Ctrl + 减号 (-) 可以快速返回之前编辑的位置，Ctrl + Shift + 减号 (-) 可以快速跳转到刚才离开的位置。

此外，你还可以根据自己的需求和编辑习惯，自定义快捷键和代码片段。具体的快捷键和代码片段设置可以在 Visual Studio 的 “工具（Tools）” -> “选项（Options）” 菜单中进行。在 “环境（Environment）” 和 “文本编辑器（Text Editor）” 选项卡下，可以找到相应的设置项。

使用快捷键 `Ctrl+M，Ctrl+O` 可以折叠当前文件中的所有代码块。

使用快捷键 `Ctrl+M，Ctrl+L` 可以展开当前文件中的所有代码块。







## Console与数据类型



### 1，控制台的类Console

Console是控制台的一个专属类

Console.WriteLine();在键盘输入，类似cout

Console.ReadKey();读取用户键盘的一个字符，主要用于暂停程序，使得程序可以手动停下

Console.ReadLine();读取一行

具体F1跳转到详细说明

![QQ截图20230620141148](picture\QQ截图20230620141148.png)

注意，下面两种效果一致

![QQ截图20230620141640](picture\QQ截图20230620141640.png)





### 2，C#数据类型的转换

![QQ截图20230620141834](picture\QQ截图20230620141834.png)

如果需要整数转化为字符串，参考下面

```c#
int a=110;
string str=a.ToString();
```





![QQ截图20230620144155](picture\QQ截图20230620144155.png)



**特别注意；；**

**从浮点型的字符串转到int     需要强转两次，否则就会报错**



### 3，数据类型的分类说明

string虽然是引用类型，但是其操作 类似 值类型

![QQ截图20230621091910](picture\QQ截图20230621091910.png)



## 托管与非托管代码

### 非托管

代码编译成功之后，依赖于特定的操作系统和CPU机器指令架构，才能执行运行

### 托管

C#代码编译之后，生成的是一种在各个操作系统都可以执行的代码，也就是中间层的代码

**.net** 里面称之为MSIL指令（微软中间语言），

然后通过操作系统的一个软件（虚拟机）将生成的中间语言最终还是翻译为CPU执行的机器指令，来执行



那么也就是说，C#的代码 将不再依赖于特定的操作系统和CPU机器指令架构，





在计算机编程中，托管代码（Managed code）和非托管代码（Unmanaged code）是描述代码执行环境和管理方式的术语。

托管代码是在托管环境下运行的代码，由托管执行环境（如.NET Framework、Java虚拟机等）负责管理内存、资源分配、安全性和垃圾回收等。托管代码运行时，执行环境会自动管理对象的创建、销毁和内存回收等操作，减轻了程序员对内存管理的负担。

非托管代码是在非托管环境下运行的代码，通常是使用本机编程语言（如C、C++）编写的代码。非托管代码需要程序员手动管理内存和资源，包括手动分配和释放内存、处理指针、资源的手动关闭等。由于没有托管执行环境提供自动内存管理和资源管理功能，非托管代码更加灵活，但同时也需要更多的注意和谨慎，以确保正确释放和管理资源，避免内存泄漏和不安全访问。

通常情况下，托管代码主要用于高级语言和框架（如C#、Java、.NET等）开发的应用程序和服务，而非托管代码主要用于操作系统、底层驱动、性能关键的部分和需要直接访问硬件的场景。

在某些情况下，为了在托管环境中与非托管代码进行交互，可以使用托管代码封装非托管代码，通过托管与非托管互操作（Interop）技术进行通信和调用非托管功能。这样可以充分发挥托管代码的便利性和安全性，并在需要时使用非托管代码的性能优势。

说明如下：：

在C#中，有两种模式：托管模式和非托管模式。

1. 托管模式（Managed mode）：在托管模式下，运行在.NET Framework或.NET Core等托管环境中。托管模式使用CLR（公共语言运行时）来管理内存分配、资源回收和安全性等。CLR负责自动处理内存管理和垃圾回收，大大简化了开发人员对内存的管理。

2. 非托管模式（Unmanaged mode）：在非托管模式下，C#代码可以直接与非托管资源进行交互，如操作系统API、COM对象和第三方C/C++库等。在非托管模式下，开发人员需要手动处理内存管理、资源释放和安全性等问题，因为CLR不会对非托管资源进行管理。

需要注意的是，尽管C#是一种高级语言，但它仍然可以与非托管代码进行交互。这为开发人员提供了更大的灵活性，使得C#可以与其他平台和语言进行互操作。但是，在使用非托管资源时，需要特别小心处理内存泄漏和资源泄漏等问题，以确保应用程序的性能和稳定性。





[vs2019 实现C#调用c++的dll两种方法_吾梦汝梦的博客-CSDN博客](https://blog.csdn.net/yumkk/article/details/106746882)

## C#调用C++ 的动态链接库

详情见3.0代码，大致说明如下

要使用C#调用C++动态库，可以通过以下步骤：

1. 创建C++动态库：首先，您需要创建一个C++动态链接库（DLL）。在C++中，使用extern "C"关键字声明的函数可以被其他语言调用。确保在导出函数时使用C链接约定，以便C#能够正确地与之交互。

2. 在C#中引用C++动态库：在C#项目中，您需要使用[DllImport]特性来声明C++动态库中的函数。该特性指定函数的名称、库文件的路径以及所需的参数。

3. 声明函数原型：在C#代码中，您需要声明C++动态库中导出函数的原型，以便C#能够正确处理函数参数和返回值。

4. 调用C++动态库函数：现在您可以在C#代码中调用C++动态库中的函数了。使用C#语法来调用通过DllImport特性引入的函数，并传递所需的参数。

请注意，调用C++动态库需要确保C++动态库可用于系统架构（例如32位或64位），并且需要正确处理参数类型和传递机制。还要注意内存管理和资源回收等问题，以确保避免内存泄漏和其他问题。

这只是一个基本的概述，具体的实现可能因库和需求而有所不同。对于更详细的指导，请参考相关的文档和资源，以了解更多关于C#调用C++动态库的详细信息和示例代码。





## C#的主函数Main形式

```c#
static void Main(string args){}

//注意，这里的void与int可随意替换，都是正确的
//    形参写或者不写也都是正确的
```





## 代码折叠器

语法如下

```c#
#region  代码标题
    
    中间代码
    
 #endregion 
```

它事实上与#if的用法有些类似，





## 一个关于整个.net(dot net)开发的概念说明

### 总体概念图

![QQ截图20230619185228](picture\QQ截图20230619185228.png)

![QQ截图20230619185304](picture\QQ截图20230619185304.png)

在安装VS时，相关的一切配置已经安装好了，类库可在项目创建时选择，虚拟机已经语言也都是配置好的



特别说明：：

VS提供在.net 平台上面运行的语言有很多种，但是最主流的是C#

C#中有大量的类库可供调用，不必自己编写，与QT提供的C++库一样

可大大节省开发时间，提高下效率，不过就是个工具罢了



### 类库以及CLR的说明：

![QQ截图20230619190512](picture\QQ截图20230619190512.png)

.net有多个类库可供选择，如  .net Framework类库

.net Framework类库  中包含各个模块可供选择，每个模块包含多个命名空间，每个命名空间中含有各自的类，可供使用



#### CLR分为CLS与CTS，说明如下：：：



![QQ截图20230619193130](picture\QQ截图20230619193130.png)

因为CLR的存在，可以将dotnet 平台所支持各种语言最终翻译成中间语言





## 自定义类库的使用说明

在VS工程中，在解决方案下面可以添加新的项目，选择添加类库，代码完成之后编译通过之后

在所需项目中添加进引入中即可，在类库后续的维护更新中，只需重新生成并且更换类库最新生成的DLL文件即可





## C#代码规范

常量的声明  要全部大写

变量的声明 小驼峰  如   studentAge   第一个单词小写，其余单词首字母大写



## 代码调试说明

鼠标移到一行，按键F9，可设置断点，或者双击这一行的最前面

F10，逐过程调试（不进入函数内部）

F11，逐步调试

F5 ，启动调试，或者执行

停止调试：：    Shift+F5 



## C#中的string说明

### 1，字符串的比较

在C#中的string，重载的==   与 ！=  运算符 比较的只是字符串的内容，而不是比较是否指代同一字符串实列（值比较）

这与C++要区分

但是在C#中  其他类型的比较，比较的都是两个变量是否指向的是同一个变量（引用比较）



### 2，string的方法使用说明，特别说明（常用操作）

Format的使用，可以格式化字符串，造就一个所需的字符串

原本是 {0}，那么可以对每一个参数给定格式化定义字符  比如  {0：C3}

![QQ截图20230620184907](picture\QQ截图20230620184907.png)



### 3，空字符串的使用

![QQ截图20230620185348](picture\QQ截图20230620185807.png)

注意，在C#中，一个没有实例化的对象是无法调用其方法和属性的

所以上面给b赋值为null时，给定NULL可以使得编译器识别其错误的调用



注意下面的结果与上面a 的结果一致

![QQ截图20230620190329](picture\QQ截图20230620190329.png)



### 4，	其他字符串的处理

![QQ截图20230620190622](picture\QQ截图20230620190622.png)

### 5，	字符串特别说明

当字符串进行+=的操作时，它会另外找一块空间存贮新生成的字符串，

那么之前的那块空间就会被无情抛弃，会占用栈空间，如下图![QQ截图20230621081211](picture\QQ截图20230621081211.png)



那么如何解决问题？？？？？

见下图

![QQ截图20230621081331](picture\QQ截图20230621081331.png)

此时的此操作可避免计算机频繁的空间浪费



### 6，	字符串的分隔 与连接

![QQ截图20230621084132](picture\QQ截图20230621084132.png)

在C#中，`Split`是一个字符串处理方法，用于将一个字符串分割成多个子字符串，基于指定的分隔符或字符数组。

`Split`的方法签名如下：

```csharp
public string[] Split(params char[] separator);
```

- `separator`: 分割字符串的字符数组或字符。可以传入多个分隔符，表示任意一个字符出现都会将字符串分割。

下面是一些示例说明：

1. 使用空格分割字符串：
```csharp
string str = "Hello World";
string[] words = str.Split(' ');
// 结果为 ["Hello", "World"]
```

2. 使用逗号分割字符串：
```csharp
string str = "Apple, Banana, Orange";
string[] fruits = str.Split(',');
// 结果为 ["Apple", " Banana", " Orange"]
```

3. 使用多个分隔符分割字符串：
```csharp
string str = "Apple;Banana|Orange";
char[] separators = new char[] { ';', '|' };
string[] fruits = str.Split(separators);
// 结果为 ["Apple", "Banana", "Orange"]
```

4. 使用字符串数组作为分隔符：
```csharp
string str = "Apple&Banana@Orange";
string[] separators = new string[] { "&", "@" };
string[] fruits = str.Split(separators, StringSplitOptions.RemoveEmptyEntries);
// 结果为 ["Apple", "Banana", "Orange"]
// StringSplitOptions.RemoveEmptyEntries 用于去除结果中的空字符串
```

需要注意的是，`Split`方法返回一个字符串数组，包含分割后的子字符串。如果需要丢弃结果中的空字符串，可以使用 `StringSplitOptions.RemoveEmptyEntries` 参数。

### 











## C#中的数组说明

### 1，基本使用

![QQ截图20230621082024](picture\QQ截图20230621082024.png)

获取数组的长度：：        数组名.Length     比如      netScore1.Length



### 2，特别说明   foreach循环的使用，如图

![QQ截图20230621082601](picture\QQ截图20230621082601.png)



### 3，引用传递（慨念与C++一样）

注意语法

![QQ截图20230621091250](picture\QQ截图20230621091250.png)







## C#中的OOP思想

### 1,类的说明

类的默认属性是私有（与C++一样）

### 2，属性的使用说明

在C#中，属性（Property）是一种特殊的成员，用于封装类中的字段，并提供对字段的访问和操作

（本质是方法），且命名时首字母必须大写。

属性通常由一个读取器（getter）和一个可选的写入器（setter）组成。读取器用于获取属性的值，写入器用于设置属性的值。属性的语法如下所示：

```csharp
public <data_type> <property_name> { get; set; }
```

其中，`<data_type>`是属性的数据类型，`<property_name>`是属性的名称。

例如，下面是一个名为`Name`的属性的示例：

```csharp
public string Name { get; set; }
```

使用属性时，可以像访问字段一样使用点语法，通过属性名称来获取或设置其值。例如：

```csharp
var person = new Person();
person.Name = "John"; // 设置属性值
string name = person.Name; // 获取属性值
```

属性可以具有不同的访问修饰符，例如`public`、`private`等，以控制属性的访问级别。此外，属性的读取器和写入器可以有不同的访问修饰符，允许更细粒度地控制属性的访问和修改。

除了自动实现的属性外，还可以**使用自定义的读取器和写入器来实现更复杂的属性逻辑**。例如：

```csharp
private string _name;
public string Name
{
    get { return _name; }
    set { _name = value.ToUpper(); }
}
```

在上述示例中，属性的写入器将输入值转换为大写，并将其存储在私有字段`_name`中。

属性的使用可以提供更好的封装性和代码可读性，以及对类成员的更好控制。

**特别注意**：：属性本身没有保存数据，数据保存在**字段**中

上面的_name 就是字段，而Name就是属性，它是对字段的快捷操作



属性的只读操作

![微信截图_20230622234417](picture\微信截图_20230622234417.png)





### 3，构造的使用

一方面，有参无参的构造与C++一致，用来初始化对象的**属性**

重点看下图

![微信截图_20230623113341](picture\微信截图_20230623113341.png)

这里在一个函数方法中，new一个对象的同时给出初始值，无参构造的一个快捷写法

这里也叫做  **对象初始化器**



### 4，对象的销毁

![微信截图_20230623114332](picture\微信截图_20230623114332.png)

在C++中一般通过析构函数释放对象所占内存，而在C#中，凭借GC后台，不需要理会

析构函数对于C#没有意义 





### 5，对象的引用改变

![微信截图_20230623114922](picture\微信截图_20230623114922.png)

**new之后会为一个对象分配空间，如果重新给定为NULL，那么意思是该指针不再指向这块内存**



### 6，接口的简单使用说明

在C#中，接口（Interface）是一种定义了一组方法、属性和事件的抽象类型。接口定义了一种契约，规定了实现该接口的类必须提供指定的成员。接口可以用于实现多态性，提供了一种灵活的方式来定义类之间的协议。

下面是使用接口的示例：

```csharp
// 定义接口
public interface IShape
{
    double CalculateArea();
    double CalculatePerimeter();
}

// 实现接口
public class Rectangle : IShape
{
    public double Width { get; set; }
    public double Height { get; set; }

    public double CalculateArea()
    {
        return Width * Height;
    }

    public double CalculatePerimeter()
    {
        return 2 * (Width + Height);
    }
}

public class Circle : IShape
{
    public double Radius { get; set; }

    public double CalculateArea()
    {
        return Math.PI * Radius * Radius;
    }

    public double CalculatePerimeter()
    {
        return 2 * Math.PI * Radius;
    }
}

// 使用接口
IShape shape1 = new Rectangle { Width = 5, Height = 10 };
IShape shape2 = new Circle { Radius = 3 };

double area1 = shape1.CalculateArea();
double perimeter1 = shape1.CalculatePerimeter();

double area2 = shape2.CalculateArea();
double perimeter2 = shape2.CalculatePerimeter();
```

上述代码中，我们定义了一个名为 `IShape` 的接口，它定义了两个方法 `CalculateArea` 和 `CalculatePerimeter`。然后我们创建了两个类 `Rectangle` 和 `Circle`，它们分别实现了 `IShape` 接口，并提供了对应的方法的具体实现。

在主程序中，我们创建了两个 `IShape` 类型的变量 `shape1` 和 `shape2`，分别引用了 `Rectangle` 和 `Circle` 的实例。通过接口变量，我们可以调用 `CalculateArea` 和 `CalculatePerimeter` 方法，而**不需要关心具体是哪个类的实例**。

这里就类似C++的父类指针指向子类对象

使用接口的好处是可以实现多态性，即可以用接口类型的变量引用不同的实现类的实例。这样可以提高代码的灵活性和可扩展性。接口还可以用于实现依赖注入、解耦合等设计模式和原则。



接口申明之后，那么该类中就应当**重写**接口类中的函数，实现自我的功能实现（多态性）





### 7，基于OOP的设计方法

1，名次分析法：怎样确定设计一个类，就看能否为这个类找到与项目相关的属性和方法（对象）,

2，确定类与类之间的关系

​	一对一，一个类作为另一个类的属性

​	一对多，一个类的多个对象作为另一个类的属性，如泛型集合（List<T>）

​	本质上关联性，一个类作为另一个类的基类

3，一个类会有固有的属性和方法的，利用参数给出不同的具体实现







## C#的方法（函数）说明

与C++大体一致，只是C++规定的访问级别的语法是一组

而C#是  **每一个方法**的返回值之前都必须要写明访问级别

且，C#与C++一样，可以**函数重载**，可以**给定默认参数**，可有**静态方法**（static声明的函数，直接属于类，通过类名调用）

![微信截图_20230623121542](picture\微信截图_20230623121542.png)



特别注意（命名参数的使用说明）
在C#中，命名参数（Named Parameters）允许我们通过参数名称来指定方法或函数的参数，而不必依赖于参数的位置顺序。这样可以提高代码的可读性，并且可以更清晰地表达参数的意图。

下面是一个使用命名参数的示例：

```csharp
public void PrintPersonDetails(string name, int age, string address)
{
    Console.WriteLine($"Name: {name}, Age: {age}, Address: {address}");
}

// 使用命名参数调用方法
PrintPersonDetails(address: "123 Main St", name: "John", age: 30);
```

在上述示例中，`PrintPersonDetails`方法接受三个参数：`name`，`age`和`address`。通过在调用方法时使用命名参数，我们可以明确指定每个参数的值，并且不必按照参数定义的顺序传递参数。

注意，使用命名参数时，参数名称必须与方法定义中的参数名称完全匹配。这样编译器才能正确地将参数值与相应的参数进行关联。

命名参数在以下情况下特别有用：

1. 当方法有多个参数，并且其中一些参数具有**默认值**时，使用命名参数可以只提供需要的参数值，而不必提供所有参数值。

2. 当方法的参数顺序不明确时，使用命名参数可以提高代码的可读性，使代码更易于理解。

3. 当方法的参数较多且相似时，使用命名参数可以减少出错的可能性。

总之，命名参数是C#中的一项有用的功能，可以提高代码的可读性和可维护性，特别是在方法调用具有多个参数或参数顺序不明确的情况下。





## C#中的容器泛型集合

总体上C#的泛型容器在概念上与C++极其类似，只是语法上不同

### 1，List的使用说明

在C#中，`List<T>`是一个非常常用的动态数组类，它提供了一组用于操作列表的方法和属性。`List<T>`类是泛型类，可以在其中存储任意类型的元素。

下面是一些常见的`List<T>`的使用示例：

1. 创建一个`List<T>`对象：

```csharp
List<int> numbers = new List<int>();
```

上述代码创建了一个名为`numbers`的`List<int>`对象，用于存储整数类型的元素。

2. 添加元素到`List<T>`中：

```csharp
numbers.Add(10);
numbers.Add(20);
numbers.Add(30);
```

上述代码使用`Add`方法将整数值添加到`numbers`列表中。

或者使用集合初始化器

```C#
List<int> numbers = new List<int>(){10,20,30};

//同时对比一下数组的初始化
int []ary=new int[]{40,50,60};

//如果要将上述数组中的数据添加到集合中呢
numbers.AddRange(ary);

//那数组与集合之间有没有更好更简洁的转换呢？？
调用方法   ToArray()    ToList()s
```



3. 访问`List<T>`中的元素：

```csharp
int firstNumber = numbers[0];
int secondNumber = numbers[1];
```

上述代码使用索引访问符（`[]`）获取`numbers`列表中的第一个和第二个元素。

4. 获取`List<T>`的长度：

```csharp
int count = numbers.Count;
```

上述代码使用`Count`属性获取`numbers`列表中的元素数量。

5. 遍历`List<T>`中的元素：

```csharp
//注意  这里的int 可以换成var
foreach (int number in numbers)
{
    Console.WriteLine(number);
}
```

上述代码使用`foreach`循环遍历`numbers`列表中的每个元素，并将其打印到控制台上。

6. 删除`List<T>`中的元素：

```csharp
numbers.Remove(20);
```

上述代码使用`Remove`方法从`numbers`列表中删除指定的元素。

7. 查找元素在`List<T>`中的索引：

```csharp
int index = numbers.IndexOf(30);
```

上述代码使用`IndexOf`方法查找元素`30`在`numbers`列表中的索引。

`List<T>`类还提供了许多其他有用的方法和属性，例如`Insert`（插入元素）、`Sort`（排序列表）、`Clear`（清空列表）等等。通过使用`List<T>`，我们可以方便地操作和管理动态数组。

8，last 方法用于获取 list中的最后一个值







### 2，集合查询的方法使用说明

在C#中，我们可以使用 LINQ（Language Integrated Query）来进行集合的快速查询和操作。LINQ 是一种强大的查询语言，它可以用于查询和操作各种数据源，包括集合、数据库、XML 等。

下面是一些常用的集合快速查询方法：

1. `Where`：根据指定的条件筛选集合中的元素。

```csharp
var result = collection.Where(x => x.Property == value);
```

上述代码使用 `Where` 方法筛选集合 `collection` 中满足条件 `x.Property == value` 的元素，并返回一个新的结果集。

2. `Select`：将集合中的每个元素根据指定的转换规则进行转换。

```csharp
var result = collection.Select(x => x.Property);
```

上述代码使用 `Select` 方法将集合 `collection` 中的每个元素的 `Property` 属性提取出来，并返回一个新的结果集。

3. `OrderBy` / `OrderByDescending`：根据指定的键对集合进行升序 / 降序排序。

```csharp
var result = collection.OrderBy(x => x.Property);
```

上述代码使用 `OrderBy` 方法根据集合 `collection` 中的 `Property` 属性对元素进行升序排序，并返回一个新的排序后的结果集。

4. `First` / `FirstOrDefault`：返回集合中满足指定条件的第一个元素。

```csharp
var result = collection.First(x => x.Property == value);
```

上述代码使用 `First` 方法返回集合 `collection` 中满足条件 `x.Property == value` 的第一个元素。如果集合中没有满足条件的元素，会抛出异常。而 `FirstOrDefault` 方法在集合中没有满足条件的元素时，会返回默认值。

5. **`Any`：判断集合中是否存在满足指定条件的元素。**

```csharp
bool result = collection.Any(x => x.Property == value);
```

上述代码使用 `Any` 方法判断集合 `collection` 中是否存在满足条件 `x.Property == value` 的元素。

6. `Count`：返回集合中满足指定条件的元素数量。

```csharp
int count = collection.Count(x => x.Property == value);
```

上述代码使用 `Count` 方法返回集合 `collection` 中满足条件 `x.Property == value` 的元素数量。

以上只是一些常用的集合快速查询方法，LINQ 还提供了许多其他方法，例如 `Skip`（跳过指定数量的元素）、`Take`（获取指定数量的元素）、`GroupBy`（根据指定的键进行分组）等等。通过使用 LINQ，我们可以简洁高效地进行集合的查询和操作。



LINQ（Language Integrated Query）是C#语言的一个特性，它提供了统一的查询语法，用于从各种数据源中检索和操作数据。LINQ允许开发人员使用类似SQL的查询表达式对数据进行过滤、排序、分组和投影等操作，而无需显式地编写循环和条件语句。

LINQ 的主要特点和组成部分如下：

1. 查询表达式语法：LINQ 提供了一种类似于SQL的查询表达式语法，使得查询代码更加简洁和易读。

   示例：
   ```csharp
   // 从数组中查询出大于 5 的数字
   int[] numbers = { 1, 3, 6, 8, 2, 10 };
   var result = from num in numbers
                where num > 5
                select num;

   foreach (int num in result)
   {
       Console.WriteLine(num);
   }
   ```

2. LINQ to Objects：允许在内存中的对象集合上执行查询操作。可以对数组、集合、列表等进行查询和操作。

   示例：
   ```csharp
   List<string> names = new List<string> { "Alice", "Bob", "Charlie", "David" };
   var result = from name in names
                where name.Length > 4
                orderby name
                select name;

   foreach (string name in result)
   {
       Console.WriteLine(name);
   }
   ```

3. LINQ to SQL：用于与关系型数据库进行交互和查询。可以通过 LINQ 查询数据库中的表和视图，并对数据进行增、删、改、查等操作。

   示例：
   ```csharp
   var result = from customer in dbContext.Customers
                where customer.Age > 18
                orderby customer.Name
                select customer;

   foreach (var customer in result)
   {
       Console.WriteLine(customer.Name);
   }
   ```

4. LINQ to XML：用于查询和操作 XML 数据。可以将 XML 数据作为对象集合并进行查询和转换。

   示例：
   ```csharp
   XDocument doc = XDocument.Load("data.xml");
   var result = from element in doc.Descendants("person")
                where (int)element.Element("age") > 18
                select element;

   foreach (var person in result)
   {
       Console.WriteLine(person.Element("name").Value);
   }
   ```

5. 其他 LINQ 提供者：除了 LINQ to Objects、LINQ to SQL 和 LINQ to XML，还可以通过其他扩展提供者实现针对其他数据源的 LINQ 查询，如 LINQ to Entities（用于 Entity Framework）和 LINQ to SharePoint（用于 SharePoint 数据）等。

通过使用 LINQ，开发人员可以以一种统一的方式对各种数据源进行查询和操作，以提高代码的可读性和可维护性。在 LINQ 中，查询操作和操作结果的延迟执行、强类型检查和编译时检查等特性也使得开发更加方便和安全。







## C#中 异常处理的语法

在C#中，异常处理可以使用try-catch语句来实现。以下是一个示例代码：

```csharp
try
{
    // 可能会抛出异常的代码块
    int a = 10;
    int b = 0;
    int result = a / b; // 这里会抛出一个除以零的异常
}
catch (Exception ex)
{
    // 捕获并处理异常的代码块
    Console.WriteLine("发生了异常：" + ex.Message);
}
finally
{
    // 可选的finally代码块，在try-catch块执行完毕后始终会被执行
    Console.WriteLine("异常处理完毕");
}
```

在上面的示例中，我们使用try关键字将可能会抛出异常的代码块包裹起来。如果在try块中发生了异常，程序会立即跳转到catch块，捕获并处理异常。在catch块中，我们可以对异常进行处理，例如打印错误信息或执行其他操作。最后，无论是否发生异常，finally块中的代码始终会被执行。

请注意，catch块中的参数ex是Exception类型，它是所有异常的基类。这意味着我们可以捕获并处理各种类型的异常。在实际的代码中，您可以根据需要使用更具体的异常类型来捕获和处理异常。



## C#中`out`、`ref`和`params`  说明

在C#中，`out`、`ref`和`params`是用来处理方法参数的关键字。

1. `out` 关键字：
   - `out` 关键字用于指定一个方法参数需要为输出参数。输出参数在方法内部必须被赋值，并在方法调用后将该值传递给调用者。
   - `out` 关键字使得方法可以返回多个值。
   - 在使用 `out` 关键字声明参数时，调用方法时必须显式传入该参数。
   - 示例：
   ```csharp
   void Divide(int dividend, int divisor, out int quotient, out int remainder)
   {
       quotient = dividend / divisor;
       remainder = dividend % divisor;
   }
   
   int dividend = 10;
   int divisor = 3;
   int resultQuotient;
   int resultRemainder;
   
   Divide(dividend, divisor, out resultQuotient, out resultRemainder);
   Console.WriteLine("Quotient: " + resultQuotient);     // 输出：Quotient: 3
   Console.WriteLine("Remainder: " + resultRemainder);   // 输出：Remainder: 1
   ```

2. `ref` 关键字：
   - `ref` 关键字用于指定一个方法参数需要按引用传递。通过 `ref` 关键字将参数传递给方法后，对参数的任何修改都会影响到调用者的变量。
   - `ref` 关键字使得**方法可以修改传入参数的值。**
   - 在调用方法时，`ref` 关键字也必须显式传入参数。
   - 示例：
   ```csharp
   void Add(ref int num)
   {
       num += 5;
   }
   
   int number = 10;
   Add(ref number);
   Console.WriteLine(number);   // 输出：15
   ```

3. `params` 关键字：
   
   - `params` 关键字用于指定一个方法可以接收可变数量的**同一类型参数**。
   - `params` 关键字只能用于方法的最后一个参数，并且只能使用一次。
   - 调用该方法时，可以传递任意数量的参数，参数将被打包为一个数组。
   - 示例：
   ```csharp
   int Sum(params int[] numbers)
   {
       int sum = 0;
       foreach (int num in numbers)
       {
           sum += num;
       }
       return sum;
   }
   
   int result = Sum(1, 2, 3, 4, 5);
   Console.WriteLine(result);   // 输出：15
   ```

这些关键字能够帮助你更灵活地处理方法的参数，使得方法可以返回多个值、修改传入参数的值或接收可变数量的参数。



## using的使用

在C#中，`using`关键字主要用于引入命名空间和管理可释放资源。以下是`using`的详细解释：

1. 引入命名空间：在C#中，命名空间是用于组织和管理类、接口、结构和其他相关类型的一种机制。使用`using`关键字可以引入一个命名空间，以便在代码中直接使用该命名空间中的类型，而无需使用完全限定名。例如：

   ```csharp
   using System; // 引入System命名空间
   
   class Program
   {
       static void Main()
       {
           Console.WriteLine("Hello, World!");
       }
   }
   ```

   在上面的例子中，我们使用`using System;`引入了System命名空间，这样我们就可以直接使用`Console`类而不需要写完全限定名`System.Console`。

2. 管理 可释放的资源：在C#中，一些对象可能会持有一些系统资源或外部资源，比如文件、数据库连接、网络连接等。为了确保在使用完这些对象后资源能够被及时释放，我们可以使用`using`语句块来简化资源管理的过程。**`using`语句块会在使用完对象后自动调用对象的`Dispose()`方法来释放资源，无论代码块是否正常执行完毕或发生异常**。例如：

   ```csharp
   using (var fileStream = new FileStream("filename.txt", FileMode.Open))
   {
       // 使用 fileStream 对象读取文件内容
   }
   ```

   在上面的例子中，我们使用`using`语句块创建了一个`FileStream`对象`fileStream`，并指定了要打开的文件名。在代码块结束时，`fileStream`对象的`Dispose()`方法会被自动调用来释放文件资源。

需要注意的是，`using`关键字在上述两种用法中具有不同的语义。在第一种用法中，`using`关键字用于引入命名空间；而在第二种用法中，`using`关键字用于资源管理。这两种用法之间没有直接关联。





## C#中实体对象的可序列化是什么意思

在C#中，对象的序列化是指将对象转换为可在网络传输或存储中使用的字节流或文本数据的过程。实体对象的序列化是一种常见的操作，它允许将对象持久化、传输或在不同应用程序之间进行交互。下面是关于C#中实体对象可序列化的详解：

1. 序列化的目的：序列化可以实现以下目的之一：

   - **持久化对象：将对象保存到磁盘或数据库中，以便将来恢复为对象。**
   
   - **远程过程调用（RPC）：通过网络传输对象，使远程应用程序能够使用这些对象。**

   - **与其他应用程序交互：将对象传递给其他应用程序，使它们能够了解和使用该对象。**

2. .NET中的序列化：在.NET框架中，使用`System.Runtime.Serialization`命名空间提供的类来实现对象的序列化和反序列化。常见的序列化方式有以下两种：

   - 二进制序列化：使用`BinaryFormatter`类将对象序列化为**二进制格式的字节流**，或从二进制字节流反序列化为对象。这种方式通**常用于.NET应用程序之间或本地文件存储之间的序列化**。

   - XML序列化：使用`XmlSerializer`类将对象序列化为**可扩展标记语言（XML）格式的文本数据**，或从XML文本反序列化为对象。这种方式**适用于与其他平台和语言进行交互的应用程序**。

3. 实体对象的可序列化：要使实体对象可序列化，需要满足以下条件：

   - 对象的类定义必须标记为**`[Serializable]`特性，表示该类是可序列化的。**

   - 对象的成员（字段、属性）也必须是可序列化的。可以**使用`[NonSerialized]`特性排除某些成员不参与序列化**。

   - **类的构造函数和方法不会被默认序列化，因为这些是行为而不是数据。**

4. 序列化示例：

   ```csharp
   [Serializable]
   public class Person
   {
       public string Name { get; set; }
       public int Age { get; set; }
   
       [NonSerialized]
       private int salary;
   
       public Person(string name, int age, int salary)
       {
           Name = name;
           Age = age;
           this.salary = salary;
       }
   }
   
   // 序列化对象
   Person person = new Person("John Doe", 30, 5000);
   BinaryFormatter formatter = new BinaryFormatter();
   using (FileStream stream = new FileStream("person.dat", FileMode.Create))
   {
       formatter.Serialize(stream, person);
   }
   
   // 反序列化对象
   BinaryFormatter formatter = new BinaryFormatter();
   using (FileStream stream = new FileStream("person.dat", FileMode.Open))
   {
       Person deserializedPerson = (Person)formatter.Deserialize(stream);
   }
   ```

   在上面的示例中，**`Person`类被标记为可序列化的(`[Serializable]`)，其中`Name`和`Age`属性被序列化，而`salary`字段被标记为不参与序列化**。使用`BinaryFormatter`类将`Person`对象序列化为二进制文件，并通过反序列化将其恢复为`Person`对象。

需要注意的是，序列化和反序列化的性能和兼容性要求会因具体的应用场景和需求而有所不同。因此，选择合适的序列化方式和设置适当的序列化选项非常重要。



![微信截图_20230719140303](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230719140303.png)





## `sealed`关键字

在C#中，`sealed`关键字用于修饰类、方法或属性，表示它们被标记为最终版本，不允许被继承、重写或复写。下面是对`sealed`关键字的详解：

1. `sealed`修饰类：通过在类的声明前加上`sealed`关键字来标记类为**密封类**。密封类是一种特殊的类，不允许其他类继承它。例如：

   ```csharp
   public sealed class MyClass
   {
       // 类定义
   }
   ```

   在上面的例子中，`MyClass`被声明为一个密封类，其他类无法继承它。密封类常用于对已存在的类进行安全封装，以防止被继承或混淆。

2. `sealed`修饰方法或属性：通过在方法或属性的声明前加上`sealed`关键字来标记它们为密封方法或属性。密封方法或属性表示它们不能在派生类中进行重写或复写。例如：

   ```csharp
   public class MyBaseClass
   {
       public virtual void MyMethod()
       {
           // 方法定义
       }
   }
   
   public class MyDerivedClass : MyBaseClass
   {
       public sealed override void MyMethod()
       {
           // 重写的方法定义
       }
   }
   ```

   在上面的例子中，`MyDerivedClass`继承自`MyBaseClass`，并且重写了`MyMethod`方法，同时使用`sealed`关键字标记该方法为密封方法，阻止其他派生类再次重写此方法。

需要注意以下几点：

- `sealed`关键字只能应用于类层次结构的最后一层。也就是说，在一个密封类或密封方法中使用`sealed`关键字申明属性和方法是无效的。

- `sealed`关键字可以使用在虚方法和抽象方法上，但是对于接口中的方法是无效的，因为接口的方法默认就是虚方法。

- 使用`sealed`关键字可以提高性能，因为编译器可以在编译时对方法进行优化。

总结来说，`sealed`关键字用于将类、方法或属性标记为最终版本，不允许继承、重写或复写。通过使用`sealed`关键字，可以提高代码安全性和性能，并阻止潜在的错误或意外重写的情况发生。



![微信截图_20230719140702](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230719140702.png)





## new关键字来(隐藏)父类中同名的方法

在C#中，可以使用`new`关键字来覆盖父类中同名的方法。`new`关键字用于隐藏基类中的成员，创建一个新的成员来覆盖相同名称的成员。使用`new`关键字覆盖父类中的成员称为"成员隐藏"。

下面是一个示例，演示了如何使用`new`关键字来覆盖父类中的同名方法：

```csharp
public class MyBaseClass
{
    public void MyMethod()
    {
        Console.WriteLine("Base class method");
    }
}

public class MyDerivedClass : MyBaseClass
{
    public new void MyMethod()
    {
        Console.WriteLine("Derived class method");
    }
}
```

在上面的示例中，`MyDerivedClass`继承自`MyBaseClass`，并使用`new`关键字**覆盖**了父类中的`MyMethod`方法。当调用`MyMethod`时，根据实际对象的类型，会调用对应的方法。

```csharp
MyBaseClass baseObj = new MyBaseClass();
MyDerivedClass derivedObj = new MyDerivedClass();

baseObj.MyMethod();    // 输出：Base class method
derivedObj.MyMethod(); // 输出：Derived class method
```

对于`baseObj`，它的类型是`MyBaseClass`，所以调用的是基类的方法。而对于`derivedObj`，它的类型是`MyDerivedClass`，所以调用的是派生类中覆盖的方法。

需要注意的是，覆盖父类方法时，子类的方法签名必须与父类的方法签名是一致的（包括返回类型、方法名和参数列表）。使用`new`关键字的**目的是明确告诉编译器子类的意图是隐藏父类的同名成员，而不是重写它**。另外，虽然使用`new`可以实现成员隐藏，但尽量避免使用这种方法，因为它可能会导致继承关系的混淆和不确定性。更好的做法是使用`override`关键字来重写基类的方法，确保代码的清晰和可维护性。



## `override`关键字详解

在C#中，`override`是一个关键字，用于在派生类中重写基类的虚方法、抽象方法或重写方法。通过使用`override`关键字，可以修改继承自基类的方法的实现逻辑。以下是对`override`关键字的详解：

1. 使用场景：`override`关键字通常用于派生类中，用于重写基类中已经声明的虚方法、抽象方法或重写方法。重写方法必须与基类方法具有相同的签名（包括返回类型、方法名和参数列表）。

2. 虚方法和抽象方法：在基类中，可以使用关键字`virtual`或`abstract`来声明虚方法或抽象方法。虚方法允许在派生类中进行重写，而抽象方法必须在派生类中进行实现。派生类使用`override`关键字来重写通过`virtual`或`abstract`关键字声明的方法。

   ```csharp
   public class MyBaseClass
   {
       public virtual void MyMethod()
       {
           // 方法定义
       }
   }
   
   public class MyDerivedClass : MyBaseClass
   {
       public override void MyMethod()
       {
           // 重写的方法定义
       }
   }
   ```

   在上面的示例中，`MyDerivedClass`继承自`MyBaseClass`，并使用`override`关键字重写了`MyMethod`方法。

3. 重写方法：在派生类中，可以使用`override`关键字重写基类中的方法。重写方法可以选择性地使用`new`关键字进行隐藏，在派生类中创建一个新的成员。

   ```csharp
   public class MyDerivedClass : MyBaseClass
   {
       public override void MyMethod()
       {
           base.MyMethod(); // 使用base关键字调用基类的方法
           // 派生类的逻辑
       }
   }
   ```

   在上面的示例中，`MyDerivedClass`重写了`MyMethod`方法，并使用`base`关键字调用了基类的方法。通过`base`关键字，可以在重写方法中访问基类的实现。

4. 虚属性和重写属性：与方法类似，可以在基类中使用虚属性，然后在派生类中使用`override`关键字进行重写。

   ```csharp
   public class MyBaseClass
   {
       public virtual int MyProperty { get; set; }
   }
   
   public class MyDerivedClass : MyBaseClass
   {
       public override int MyProperty { get; set; }
   }
   ```

   在上述示例中，`MyDerivedClass`重写了基类中声明的虚属性`MyProperty`。

使用`override`关键字能够确保在派生类中正确地重写基类的虚方法、抽象方法或重写方法，并为这些方法提供新的实现逻辑。这是C#中实现多态性的基本机制之一，它允许在运行时根据对象的实际类型来调用正确的方法。



## readonly

`readonly` 是 C# 中的关键字，用于修饰字段（Field）或变量（Variable）。当字段或变量被声明为 `readonly` 时，**表示该字段或变量只能在声明时或构造函数中进行初始化，并且不能在其他地方进行赋值操作。**

具体来说，`readonly` 关键字有以下特点：

1. 只能在字段声明时或构造函数中对字段进行初始化。**一旦字段被初始化，就无法再修改其值**。
2. 可以在声明语句或构造函数中进行初始化，但不能在属性访问器、方法中或其他地方进行赋值操作。
3. `readonly` 字段的值可以是编译时常量或运行时常量，也可以是一个表达式，但必须在构造函数中确定其值。
4. `readonly` 修饰符仅用于实例字段，**不能用于静态字段。**

使用`readonly`关键字可以确保在程序执行过程中，被声明为`readonly`的字段的值不会被无意间更改，提供了更多的安全性和可靠性。通常，`readonly`关键字用于标识不可更改的常量或只读属性的 backing field（支持字段）。





## default

当使用default关键字时，您可以通过以下方式使用它：

1. 默认变量初始化：

```csharp
int age = default; // 将age初始化为int类型的默认值，即0
bool isTrue = default; // 将isTrue初始化为bool类型的默认值，即false
string name = default; // 将name初始化为string类型的默认值，即null
```

2. 泛型类型参数：

```csharp
public T GetDefaultValue<T>()
{
    return default(T); // 返回类型T的默认值
}

int defaultValue = GetDefaultValue<int>(); // defaultValue将被赋值为int类型的默认值，即0
string defaultString = GetDefaultValue<string>(); // defaultString将被赋值为string类型的默认值，即null
```

3. switch语句的默认情况：

```csharp
int day = 7;

switch (day)
{
    case 1:
        Console.WriteLine("Monday");
        break;
    case 2:
        Console.WriteLine("Tuesday");
        break;
    // ...
    default:
        Console.WriteLine("Invalid day");
        break;
}
```

在上述示例中，如果day的值既不是1也不是2，则执行default语句块。

4. 可空类型：

```csharp
int? nullableInt = default; // nullableInt将被赋值为null，因为int?是可空类型
decimal? nullableDecimal = default(decimal?); // nullableDecimal将被赋值为null，类型为decimal?的默认值
```

在这个示例中，我们使用了可空类型int?和decimal?来存储null值，使用default关键字将这些可空类型初始化为null。

总之，default关键字在C#中可以用于初始化变量的默认值，定义泛型类型参数的默认值，处理switch语句中的默认情况，以及在可空类型中表示null值。





## 操作路径的类  Path





## Dictionary



在 C# 中，Dictionary 类型是基于哈希表实现的字典集合。

区别：
1. 接口：Dictionary 是 C# 的一种集合类型，而哈希表是一种数据结构。
2. 键值对的存储：Dictionary 使用键值对的方式来存储和访问数据，而哈希表则使用哈希函数将键映射到数组索引位置。
3. 顺序：Dictionary 不保持插入元素的顺序，而哈希表也没有严格的顺序保证。
4. 扩展性：Dictionary 提供了一些额外的成员和功能，例如 TryGetValue 方法、LINQ 查询等。哈希表的功能相对较少。

联系：
1. 底层数据结构：Dictionary 类型和哈希表都是使用哈希表作为底层的数据结构来实现的。
2. 快速查找：由于哈希表使用哈希函数进行键的映射，可以快速根据键查找和访问数据。

总的来说，Dictionary 类型是**基于哈希表实现的高级数据结构**，提供了更多的功能和灵活性，而哈希表是一种更基础、更底层的数据结构，用于快速查找和访问数据。



在C#中，Dictionary是一种用于存储键值对的集合类型。它是泛型类型，允许您指定键和值的数据类型。

以下是一个简单的示例，演示了如何创建和使用Dictionary：

```csharp
using System;
using System.Collections.Generic;

public class Program
{
    public static void Main()
    {
        // 创建一个Dictionary实例
        Dictionary<string, int> studentGrades = new Dictionary<string, int>();

        // 向Dictionary添加键值对
        studentGrades.Add("Alice", 85);
        studentGrades.Add("Bob", 92);
        studentGrades.Add("Charlie", 78);

        // 获取特定键的值
        int grade = studentGrades["Bob"];
        Console.WriteLine("Bob的成绩: " + grade);

        // 检查字典中是否存在指定的键
        bool isMaryPresent = studentGrades.ContainsKey("Mary");
        Console.WriteLine("Mary在字典中存在吗？" + isMaryPresent);

        // 使用foreach循环遍历字典中的所有键值对
        foreach (var kvp in studentGrades)
        {
            Console.WriteLine(kvp.Key + "的成绩: " + kvp.Value);
        }
    }
}
```

在上述示例中，我们首先创建了一个泛型Dictionary实例，其键的类型为string，值的类型为int。然后，我们使用Add方法向Dictionary添加键值对，并使用索引器语法访问指定键的值。另外，可以使用ContainsKey方法检查字典中是否存在指定的键，并使用foreach循环遍历字典中的所有键值对。

Dictionary的使用非常灵活，可以根据需要添加、更新、删除和查找键值对。它是一个强大且常用的数据结构，特别适用于需要通过键来快速访问和操作数据的场景。

Dictionary类提供了一系列通用的方法，用于添加、获取、更新和删除键值对等操作。以下是一些最常用的方法：

1. Add(key, value)：向字典中添加指定的键值对。
2. ContainsKey(key)：判断字典中是否包含指定的键。
3. ContainsValue(value)：判断字典中是否包含指定的值。
4. Remove(key)：从字典中移除指定的键值对。
5. TryGetValue(key, out value)：尝试从字典中获取与指定键关联的值，如果键存在，则将对应的值返回。
6. Clear()：清空字典，移除所有的键值对。
7. Count：获取字典中键值对的数量。
8. Keys：获取字典中所有的键。
9. Values：获取字典中所有的值。
10. GetEnumerator()：返回一个可以用于循环遍历字典的枚举器。

除了上述方法之外，Dictionary还提供了一些其他的辅助方法和属性，用于特定的需求，如LINQ扩展方法、索引器（索引访问）、序列化和反序列化等。

请记住，Dictionary类是根据键唯一性进行散列存储和快速查找的，因此键的类型需要实现正确的哈希码和相等性比较方法（GetHashCode和Equals），以确保字典的工作正常。

根据不同的需求，您可以选择使用Dictionary类提供的适当方法来操作键值对，以满足您的编程需求。



特别的，可以考虑 

```C# 
Dictionary<string, object> 
```

类似这种，好用



在 C# 中，`Dictionary<TKey, TValue>` 属于泛型集合，是一个存储键值对的集合，这里的 TKey 是字典键的类型，TValue 是与键相关联的值的类型。`Dictionary<TKey, TValue>` 在 System.Collections.Generic 命名空间中。

下面是 `Dictionary<TKey, TValue>` 的使用说明：

1. **引入命名空间**：
   ```csharp
   using System.Collections.Generic;
   ```

2. **创建 Dictionary**：
   ```csharp
   Dictionary<int, string> myDictionary = new Dictionary<int, string>();
   ```

3. **添加元素**：
   使用 `Add` 方法添加元素到字典。如果键已经存在会抛出一个 `ArgumentException`。
   ```csharp
   myDictionary.Add(1, "One");
   myDictionary.Add(2, "Two");
   // ...
   
   // 另一种检查键是否存在的方式是使用索引运算符，但这会覆盖原有键对应的值
   myDictionary[3] = "Three"; // 如果键 3 存在，会覆盖；不存在，会添加。
   ```

4. **删除元素**：
   `Remove` 方法通过键来删除元素。
   ```csharp
   myDictionary.Remove(2); // 删除键为 2 的元素
   ```

5. **查找元素**：
   使用 `ContainsKey` 方法来检查是否包含某个键。
   ```csharp
   if (myDictionary.ContainsKey(1)) {
       // 键存在
   }
   ```

   使用 `TryGetValue` 方法尝试获取与键相关联的值，如果键存在，返回 true；否则返回 false，并且 out 参数返回 TValue 的默认值。
   ```csharp
   string value;
   if (myDictionary.TryGetValue(1, out value)) {
       // 成功找到键，并获取值
   }
   ```

6. **访问元素**：
   通过键直接访问。
   ```csharp
   string value = myDictionary[1]; // 获取键 1 对应的值，如果键不存在会抛出一个 KeyNotFoundException
   ```

7. **修改元素**：
   通过键直接赋值来修改字典中的元素。
   ```csharp
   myDictionary[1] = "OneUpdated"; // 将键 1 对应的值更新为 "OneUpdated"
   ```

8. **遍历 Dictionary**：
   可以使用 `foreach` 循环来遍历键值对。
   ```csharp
   foreach (KeyValuePair<int, string> kvp in myDictionary) {
       Console.WriteLine("Key = {0}, Value = {1}", kvp.Key, kvp.Value);
   }
   ```

   也可以单独遍历字典中的键或值。
   ```csharp
   foreach (int key in myDictionary.Keys) {
       // 遍历键
   }
   
   foreach (string value in myDictionary.Values) {
       // 遍历值
   }
   ```

9. **清空 Dictionary**：
   清空字典中的所有元素。
   ```csharp
   myDictionary.Clear(); // 清空字典
   ```

10. **获取元素数量**：
    使用 `Count` 属性来获取字典中元素的数量。
    ```csharp
    int count = myDictionary.Count; // 获取字典中的元素个数
    ```

`Dictionary<TKey, TValue>` 在内部使用哈希表来存储数据，因此它的查找和添加操作的平均时间复杂度接近于 O(1)。但是要确保 TKey 类型区分良好的哈希代码，以便维护这种性能。

请注意，`Dictionary<TKey, TValue>` 不保证元素的顺序，如果需要有序字典可以使用 `SortedDictionary<TKey, TValue>` 类。

如果您想了解更多关于 `Dictionary<TKey, TValue>` 类的高级用法和注意事项，请参考以下几点：

### 线程安全
`Dictionary<TKey, TValue>` 不是线程安全的。如果需要在多线程环境中使用，可以考虑使用 `ConcurrentDictionary<TKey, TValue>` 类，位于 `System.Collections.Concurrent` 命名空间，它提供了线程安全的字典操作。

### 自定义对象作为键
如果您使用自定义对象类型作为键 (`TKey`)，那么您需要确保正确地实现了这个类型的 `GetHashCode` 和 `Equals` 方法，因为 `Dictionary<TKey, TValue>` 使用这些方法来确定键的唯一性。

### 使用值类型作为键
当值类型（如 `int`, `double`, `struct` 等）作为字典的键时，请注意值类型的装箱和拆箱操作，它们可能影响性能。特别是使用结构体作为键时，确保它不会因为频繁的复制而导致性能问题。

### 序列化与反序列化
如果您需要将 `Dictionary<TKey, TValue>` 对象进行序列化和反序列化（例如，保存到文件或通过网络传输），请确保键和值的类型都是可序列化的。

### 容量与性能
字典的容量会随着元素的添加自动增长。如果您事先知道将要存储的元素数量，可以在创建字典时指定初始容量，以减少重新哈希的次数和提高性能。

```csharp
int initialCapacity = 100;
Dictionary<int, string> myDictionary = new Dictionary<int, string>(initialCapacity);
```

### 查找性能
如果频繁地对字典进行查找操作，要确保如果使用字符串作为键时，考虑使用 `StringComparer.OrdinalIgnoreCase` 或适当的 `StringComparer`。这样可以减少因大小写转换所付出的性能代价。

```csharp
Dictionary<string, string> myDictionary = new Dictionary<string, string>(StringComparer.OrdinalIgnoreCase);
```

### 比较器的使用
可以自定义 `IEqualityComparer<TKey>` 接口的实现来自定义比较器，然后将其传递给字典，以自定义键的比较逻辑。

### 集合的视图
`Dictionary<TKey, TValue>.KeyCollection` 和 `Dictionary<TKey, TValue>.ValueCollection` 类型提供了对字典键和值的集合的视图。这些视图是动态的；即，它们反映了对字典的更改。

### LINQ 与字典
`Dictionary<TKey, TValue>` 是可以与 LINQ (Language Integrated Query) 一起使用的，因此您可以轻松地查询字典或进行变换。

```csharp
var filteredDictionary = myDictionary.Where(kvp => kvp.Value.StartsWith("One"))
                                    .ToDictionary(kvp => kvp.Key, kvp => kvp.Value);
```

请记住，LINQ 查询返回的是集合的副本，而不是原始集合的直接视图。

使用 `Dictionary<TKey, TValue>` 类时了解这些概念和技巧将帮助您更有效地使用这个强大的集合类型。

除了前面提到的详细使用说明和高级用法，以下是一些其他相关的点，这些点也可以提高 `Dictionary<TKey, TValue>` 使用体验：

### 复杂度
`Dictionary<TKey, TValue>` 实例的查找、添加和删除操作的平均时间复杂度是 O(1)。然而，在最坏情况下，这些操作的时间复杂度可能会退化到 O(n)，其中 n 是字典中的元素数。这种情况通常发生在提供的哈希函数产生了太多的冲突时。

### 哈希码
键的哈希码是通过 `GetHashCode` 方法得到的，这个方法返回一个 32 位整数。哈希表使用这个哈希码来快速查找键值对。为了避免冲突和维持字典性能，确保 `GetHashCode` 方法提供的哈希码可以均匀地分散。

### 并发修改
在对 `Dictionary<TKey, TValue>` 进行枚举时，如果字典内容被修改，比如添加或删除元素，这会导致 `InvalidOperationException`。如果您需要在枚举时修改集合，可以先将元素拷贝到另一集合，再对其进行修改操作。

### Capacity 和 Count 属性
字典的 `Capacity` 属性是字典可以储存的元素的总数，而 `Count` 属性是字典当前包含的键值对数目。调整 `Capacity` 可以提高大量添加操作后的性能。

### 使用 `KeyValuePair<TKey, TValue>` 结构
当遍历 `Dictionary<TKey, TValue>` 时，您会遍历 `KeyValuePair<TKey, TValue>` 实例。这是一个结构体，包含一个不可变的键和一个可变的值。您可以读取 `Key` 属性，但不能设置它，因为它是只读的。

### 其他集合与字典的互操作
您可以使用 LINQ 或其他方法将其他集合转换为字典。如果有一个列表或数组，可以使用 `ToDictionary` 扩展方法将其转换为 `Dictionary<TKey, TValue>`。

### 复制字典
如果你需要一个字典的副本，你可以使用字典构造函数或者 LINQ 来创建一个新的字典。

### 字典和 JSON
字典很容易转换为 JSON 格式，并在 Web API 中使用。序列化和反序列化可通过类似 Newtonsoft.Json 或 System.Text.Json 提供的功能进行。

确保在使用 `Dictionary<TKey, TValue>` 类时，充分理解其特性和行为，这样可以编写出更健壮、可靠和高性能的代码。

### 相等性的处理
当比较键的相等性时，字典使用 `EqualityComparer<TKey>.Default`。对于大多数类型来说，这等同于调用对象的 `Equals` 和 `GetHashCode` 方法。如果你的键类型是引用类型，并且你希望字典以引用相等性来比较键，你需要提供一个自定义的 `IEqualityComparer<T>` 实例。

### 只读字典
如果你想防止字典被修改，可以使用 `ReadOnlyDictionary<TKey, TValue>` 包装你的字典。这是在 `System.Collections.ObjectModel` 命名空间中。

```csharp
var readOnlyDict = new ReadOnlyDictionary<TKey, TValue>(myDictionary);
```

### 避免大量删除操作带来的性能问题
如果你的用例涉及到大量的删除操作，当删除项是大量非连续内存块时，性能可能会下降，因此在某些情况下，重新创建字典可能比删除许多项更高效。

### 自定义字典
如果 `Dictionary<TKey, TValue>` 类提供的功能不足以满足需求，你可以继承它并添加自定义行为，或者实现 `IDictionary<TKey, TValue>` 接口来从头开始构建自己的字典结构。

### 存储空间优化
如果存储的键和值的类型占用的存储空间很大，或者你要处理的字典数量非常多，那么考虑存储空间优化将很有必要。比如使用值类型而不是对象或者使用引用类型的 ‘struct’ 来减少内存消耗。

### 诊断性能问题
如果你遇到了字典性能问题，确保诊断是否是因为哈希码冲突导致的，你可以统计存储桶（内部数组）的使用情况，来看是否均衡分布。如果不是，那可能你需要重新设计键的哈希函数，或者考虑使用其他类型的数据结构。

### 内存消耗评估
当处理大规模数据时，请注意 `Dictionary<TKey, TValue>` 的内存消耗。随着集合增长，它将需要更多的内存，可能导致 `OutOfMemoryException`，确保你的应用程序可以高效地处理内存。

### `TryGetValue` 和 `ContainsKey` 方法
在尝试从字典中检索值时，推荐使用 `TryGetValue` 方法，它提供了一种安全的方式来尝试获取与给定键相关联的值，而不会抛出异常。

### 序列化注意事项
如果你需要自定义序列化行为，比如在字典中使用非序列化对象或需要以特别的格式序列化，你可能需要实现自定义序列化和反序列化逻辑。

最后，始终根据你的实际需求来选择合适的数据结构。`Dictionary<TKey, TValue>` 是一种非常灵活和强大的数据结构，但也不是对所有用例都是最佳选择。评估你的应用程序的特定需求，并确定 `Dictionary` 是否是解决这些问题的最佳方式。如果需要，也可以考虑 `SortedList<TKey, TValue>`，`SortedDictionary<TKey, TValue>` 等其他集合类型。

### 调试支持
在调试过程中，`Dictionary<TKey, TValue>` 类有内置的调试视图，如 `Mscorlib_CollectionDebugView`，它可以帮助你更好地查看字典在调试时的状态，例如查看当前的键值对、存储桶信息等。这对于诊断问题或理解字典的运行情况非常有用。

### 线程安全
`Dictionary<TKey, TValue>` 本身不是线程安全的。如果你需要在多线程环境中访问字典，并且操作必须是原子的，可以考虑使用 `ConcurrentDictionary<TKey, TValue>` 类，它在 `System.Collections.Concurrent` 命名空间中提供，并为多线程场景专门设计。

```csharp
var concurrentDictionary = new ConcurrentDictionary<TKey, TValue>();
```

### 序列化和反序列化
当涉及到序列化和反序列化字典时（例如，使用 JSON），请确保字典的键是可序列化的。对于复杂类型的键，请确保正确实现了序列化关键方法`（如 ToString()` 和 `GetHashCode`）以便能够正确地序列化和反序列化。

### 文化敏感性
如果键是字符串类型，那么进行哈希和比较时考虑文化敏感性可能很重要。默认的比较器不考虑区域性，但在某些情况下，你可能需要一个考虑到文化特定规则的比较器。

### 可变键的风险
如果你使用可变类型（其属性或字段可以改变的类型）作为键，那么一旦键值改变，可能会影响键的哈希码，从而使原键值对在字典中无法找到。避免使用可变对象作为字典键可以避免此类问题。

### 内存敏感的应用
在内存敏感的应用程序中，务必注意 `Dictionary<TKey, TValue>` 的内存用量。设置合适的初始容量和负载因子，以优化内存使用，特别是在处理大量的小型字典时。

### 扩展方法
字典可以与 LINQ 配合使用，提供强大的查询和操作功能。可以用 LINQ 扩展方法如 `Where`, `Select`, `Aggregate` 等对字典进行操作，实现功能更为丰富和灵活的数据处理。

### 性能测试
在关键性能场景中使用字典前，建议进行充分的性能测试。这包括评估内存占用、操作的响应时间以及在极端条件下的性能表现。

结合以上的考虑因素，您可以制定策略以确保`Dictionary<TKey, TValue>`的使用尽可能地与您的场景和需求匹配。务必记住，在涉及到性能、内存管理、线程安全、键管理和序列化等关键系统特性时，理解和正确使用字典是至关重要的。







## 接口的使用说明



![微信截图_20230719162726](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230719162726.png)



在C#中，接口（interface）是一种用于定义方法、属性、事件和索引器的合约。它定义了一组行为，但并不提供任何实现细节。下面是对C#中接口的详解：

1. 接口的声明：接口使用`interface`关键字进行声明，并且不能包含字段或具体实现代码。

   ```csharp
   public interface IMyInterface
   {
       void MyMethod();
       int MyProperty { get; set; }
       event EventHandler MyEvent;
   }
   ```

   在上面的示例中，定义了一个名为`IMyInterface`的接口，它包含了一个无返回值、无参数的方法`MyMethod`，一个带有读写访问器的属性`MyProperty`，以及一个事件`MyEvent`。

2. 实现接口：在类中使用关键字`implements`来实现一个或多个接口。实现接口意味着类要遵循接口定义的行为，并提供每个接口成员的实现。

   ```csharp
   public class MyClass : IMyInterface
   {
       public void MyMethod()
       {
           // 方法实现
       }
   
       public int MyProperty { get; set; }
   
       public event EventHandler MyEvent;
   }
   ```

   在上述示例中，`MyClass`类实现了`IMyInterface`接口，并提供了接口中定义的所有成员的具体实现。

3. 多接口实现：一个类可以同时实现多个接口，用逗号分隔接口的名称。

   ```csharp
   public class MyClass : IInterface1, IInterface2
   {
       // 实现接口的成员
   }
   ```

4. 显式接口实现：当一个类实现了多个接口，且这些接口拥有相同的成员名称时，可以使用显式接口实现来明确指定每个接口成员的实现。

   ```csharp
   public class MyClass : IInterface1, IInterface2
   {
       void IInterface1.MyMethod()
       {
           // IInterface1中MyMethod的具体实现
       }
   
       void IInterface2.MyMethod()
       {
           // IInterface2中MyMethod的具体实现
       }
   }
   ```

   在上述示例中，`MyClass`类实现了`IInterface1`和`IInterface2`接口，并通过显式接口实现为每个接口的`MyMethod`提供了不同的具体实现。

5. 接口继承：接口可以继承其他接口，通过冒号分隔多个接口的名称。

   ```csharp
   public interface IDerivedInterface : IBaseInterface
   {
       // 新接口成员
   }
   ```

   上述示例中，`IDerivedInterface`接口继承了`IBaseInterface`接口，并可以定义新的接口成员。

使用接口的好处是可以实现多态性和代码重用。接口提供了一种约定，定义了类应该具备的行为。类通过实现接口来遵循这种约定，从而实现了接口所描述的行为。通过接口，可以实现类与类之间的松耦合，增加代码的灵活性和可维护性。



6，接口的多态性：通过接口，你可以使用多态性来处理不同实现了相同接口的对象。

```c#
IMyInterface obj1 = new MyClass1();
IMyInterface obj2 = new MyClass2();

obj1.MyMethod(); // 调用 MyClass1 中实现的 MyMethod()
obj2.MyMethod(); // 调用 MyClass2 中实现的 MyMethod()
```



![微信截图_20230719170048](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230719170048.png)





![微信截图_20230719170339](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230719170339.png)

这里就类似C++中   **父类指针指向子类对象**,子类对象会调用具体的实现

继承多态是指：：传参时，父类指针指向子类对象，实参是子类对象，子类中重写父类中的虚函数或抽象方法

接口多态是指：：

![微信截图_20230719173233](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230719173233.png)





 ![微信截图_20230719172358](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230719172358.png)





![微信截图_20230719173947](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230719173947.png)







## 反射的使用说明

[c#之反射详解_c#反射_鲤籽鲲的博客-CSDN博客](https://blog.csdn.net/qq_39847278/article/details/129816667)

![微信截图_20230720205257](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230720205257.png)

反射

![微信截图_20230802152054](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230802152054.png)





### 反编译的概念

反编译是指将已经编译过的程序代码   转换  回其原始源代码的过程。在这种情况下，是指将已经编译成中间语言（Intermediate Language，简称IL）的代码转换回其原始的源代码。

IL代码是一种中间语言，它是在编译过程中生成的，用于在不同的平台上执行。通过反编译IL代码，可以查看程序的源代码，理解其逻辑和功能。这对于理解和学习程序代码、进行代码分析和调试等都非常有帮助。



## 特性

为程序元素额外添加声明信息的一种方式，或者说声明一个标签，给他的使用者起一个别名

通过给属性或者类一个特性标签

那么在反射时，就可以根据标签来判断进行什么样的操作

[CallerMemberName] 许可你这个形参有默认值，并且可以从属性直接得到属性名作为参数





## 委托

![企业微信截图_20230726160040](D:\黄浒烨\TY--MD文件\C#\picture\企业微信截图_20230726160040.png)



![微信截图_20230726171805](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230726171805.png)

![微信截图_20230726171943](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230726171943.png)

![微信截图_20230726172250](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230726172250.png)

注意：在实际应用中，在A类中创建一个委托，在B类中创建一个A的实例，在这个实例的委托关联B中的函数，那么在A中执行的委托就会执行B中关联的函数（建立一个连接）

委托中会有一个invoke方法，可以使得委托关联的所有函数全部执行

委托最核心的用处在于，当你当前无法直接调用你想要的方法时 ，你可以申明一个委托去关联

特别注意：：：   你要先申明一个委托，然后在用委托实例化一个对象，用这个对象关联你要的函数





在C#中，delegate（委托）是一种数据类型，它可以用来引用或封装一个或多个方法，并允许将这些方法当做参数传递、存储在变量中或作为返回值返回。

委托的声明基本语法如下：
```csharp
delegate returnType DelegateName(parameters);
```
- `returnType` 表示委托所引用方法的返回类型。
- `DelegateName` 是委托的名称。
- `parameters` 是方法参数列表。

委托的用途是在运行时动态地将方法调用与方法实现分开，通过委托可以实现事件处理、回调函数等高级编程技术。

以下是委托的主要用法和特性：

1. 声明委托类型：在定义委托类型时，需要确定委托引用的方法签名，包括返回类型和参数列表。
```csharp
delegate void MyDelegate(string message);
```

2. 委托的实例化：用方法实例化委托，即将方法赋给委托变量，使委托持有对该方法的引用。
```csharp
MyDelegate myDelegate = new MyDelegate(MyMethod);
```

3. 委托的调用：通过委托变量调用引用的方法，可以像调用普通方法一样调用委托。
```csharp
myDelegate("Hello"); // 调用委托引用的方法
```

4. 委托的多播（Multicast：委托可以同时引用一个以上的方法，多个方法按照添加的顺序依次被调用。
```csharp
myDelegate += AnotherMethod; // 添加方法到委托的调用列表
myDelegate("Hello"); // 调用委托引用的多个方法
```

5. 委托作为参数：委托可以作为方法的参数传递，实现回调函数的功能。
```csharp
void ProcessData(string data, MyDelegate callback)
{
    // ... 处理数据
    callback(data); // 调用回调函数
}
```

6. 委托作为返回值：方法可以返回委托作为结果，以供后续调用。
```csharp
MyDelegate GetDelegate()
{
    return new MyDelegate(MyMethod);
}
```

7. 内置委托类型：C#提供了一些内置的委托类型，如 `Action`、`Func` 和 `Predicate`，可以方便地引用不同类型的方法。

使用委托可以实现灵活的事件处理、异步编程和回调机制等。它是C#中重要的特性之一，能够提高代码的可扩展性和复用性。















## 事件

在C#中，`event` 是一种特殊的成员，用于定义和使用事件。事件是一种机制，允许对象在发生特定的操作或状态改变时，通知其他对象。

以下是关于 C# 中 `event` 的详细说明：

1. 事件的声明：使用 `event` 关键字来声明一个事件。**通常与委托类型进行关联，指定事件可以触发的特定委托类型**。
```csharp
event EventHandler MyEvent;
```

2. 事件的订阅与取消订阅：通过使用 `+=` 运算符添加事件处理程序（委托的实例），使用 `-=` 运算符取消事件处理程序。
```csharp
object.MyEvent += EventHandlerMethod; // 订阅事件
object.MyEvent -= EventHandlerMethod; // 取消订阅事件
```

3. 触发事件：通过调用事件的方法，即通过 `event` 成员的委托进行调用。通常由事件发布者在适当的时间调用。
```csharp
MyEvent(this, EventArgs.Empty); // 触发事件，并传递特定的参数
```

4. 事件委托类型：事件需要一个委托类型来定义事件处理程序的签名，指定事件处理程序接受的参数和返回值。
```csharp
public delegate void EventHandler(object sender, EventArgs e);
```

5. 事件的命名规范：事件名称通常使用 PascalCase（首字母大写）来命名，并以 `event` 作为前缀。
```csharp
public event EventHandler MyEvent;
```

事件的使用可以实现许多常见的编程模式，如观察者模式、发布-订阅模式等，使对象之间能够以松散耦合的方式进行通信和交互。事件提供了一种灵活且可扩展的方式来处理对象之间的通知和响应。







## Lambda



![微信截图_20230726195601](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230726195601.png)



![微信截图_20230726195909](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230726195909.png)







注意观察下面代码，对比区别

![微信截图_20230726201811](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230726201811.png)

![微信截图_20230726201822](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230726201822.png)

```C#
public delegate T MyGenericDeleage<T>(T a,T b)
//注意  MyGenericDeleage<T>  这里的<T>  表示T是一个数据类型，
// MyGenericDeleage<T>中  表示MyGenericDeleage是一个泛型委托
```





微软官方提供了一些泛型委托，已经在系统空间中定义好了，可以直接指定参数类型，直接用即可，无需额外在定义一次

详情如下

**Func委托**

![微信截图_20230727084411](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230727084411.png)





参考一个用法

![微信截图_20230727191623](D:\黄浒烨\TY--MD文件\C#\picture\微信截图_20230727191623.png)



这里的**`FindAll`**  就是一个委托，既然是委托，那么就可以用Lambda  表达式





## LINQ

### IEnumerable接口的详解

[IEnumerable（C#）_c# ienumerable_♡XXXX.yee的博客-CSDN博客](https://blog.csdn.net/qq_64410237/article/details/131695354)



[C#中的LINQ_c# linq_青柚172的博客-CSDN博客](https://blog.csdn.net/qq_71012549/article/details/128332144)

[C#中的LINQ_c# linq_Hello Bug.的博客-CSDN博客](https://blog.csdn.net/LLLLL__/article/details/120605415)



[C#中Linq用法汇集_c# linq_kalvin_y_liu的博客-CSDN博客](https://blog.csdn.net/kalvin_y_liu/article/details/125506763)



当使用C#中的LINQ查询语句时，可以使用Queryable和Lambda两种写法。下面是几个例子，分别展示了使用Queryable和Lambda的C# LINQ查询语句中的where、group、select和orderby子句的用法。

1. Where子句的Queryable写法：

```csharp
// Queryable
var query = from person in dbContext.Persons
            where person.Age > 18
            select person;

// Lambda
var query = dbContext.Persons.Where(person => person.Age > 18);
```

2. Group子句的Queryable写法：

```csharp
// Queryable
var query = from person in dbContext.Persons
            group person by person.City into cityGroup
            select new { City = cityGroup.Key, Count = cityGroup.Count() };

// Lambda
var query = dbContext.Persons
            .GroupBy(person => person.City)
            .Select(cityGroup => new { City = cityGroup.Key, Count = cityGroup.Count() });
```

3. Select子句的Queryable写法：

```csharp
// Queryable
var query = from person in dbContext.Persons
            where person.Age > 18
            select new { person.Name, person.Age };

// Lambda
var query = dbContext.Persons
            .Where(person => person.Age > 18)
            .Select(person => new { person.Name, person.Age });
```

4. OrderBy子句的Queryable写法：

```csharp
// Queryable
var query = from person in dbContext.Persons
            orderby person.Name ascending
            select person;

// Lambda
var query = dbContext.Persons.OrderBy(person => person.Name);
```

以上示例分别展示了Queryable和Lambda表达式的写法，您可以根据自己的喜好和需求选择使用哪种写法。







## 异步编程

invoke     激发

在C#中，异步调用是指一种编程模式，可以在进行I/O操作、网络请求或者其他耗时操作时，以**非阻塞**的方式执行代码。异步调用可以提高程序的响应性能，**因为主线程在等待异步操作完成的同时可以执行其他任务**。



在C#中，使用`async`和`await`关键字来实现异步调用。以下是一个示例：

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main(string[] args)
    {
        await DownloadContentAsync();
        
        Console.WriteLine("其他任务可以继续执行...");
        Console.ReadLine();
    }
    
    public static async Task DownloadContentAsync()
    {
        using (HttpClient client = new HttpClient())
        {
            string result = await client.GetStringAsync("https://www.example.com");
            Console.WriteLine(result);
        }
    }
}
```

在上面的示例中，`Main`方法内使用`await`关键字来等待`DownloadContentAsync`方法的执行完成。`DownloadContentAsync`方法内部使用`await`关键字等待`HttpClient.GetStringAsync`方法返回结果。

异步调用通常返回`Task`或`Task<T>`类型的对象，它们表示异步操作的执行状态和结果。**通过`await`关键字对这些对象进行等待，可以阻塞当前方法并允许其他任务（调用这个await的这个函数的外面，比如说上面的第11行代码）并允许其他工作在异步操作执行期间继续进行   继续执行。**

需要注意的是，**在使用异步调用时，必须在方法签名上加上`async`修饰符**，**以及在方法内部使用`await`关键字来等待异步操作的完成。**这样才能够正确地使用异步调用的功能。





在 C# 中，异步操作使你能够编写更高效和响应性的代码，可以在进行耗时的操作时不阻塞主线程，提高程序的性能和用户体验。下面是有关 C# 中异步操作的详解：

1. **异步方法声明：** 使用 `async` 关键字来声明异步方法。异步方法通过 `Task` 或 `Task<T>` 返回结果。

   ```csharp
   public async Task<int> CalculateSumAsync(int a, int b)
   {
       // 异步代码
       int sum = await LongRunningCalculationAsync(a, b);
       return sum;
   }
   ```

   `Task<T>` 表示异步操作返回一个值，而 `Task` 表示异步操作不返回结果。

2. **异步方法调用：** 调用异步方法时，使用 `await` 关键字等待方法的完成。此时，控制权将返回给调用方，不会阻塞主线程。

   ```csharp
   int result = await CalculateSumAsync(3, 5);
   ```

   在异步代码中，当遇到 `await` 表达式时，**当前方法将暂停  并允许其他工作在异步操作执行期间继续进行**。

3. **异步事件处理：** 使用 `async` 关键字声明异步事件处理程序时，事件处理程序可以在异步方式下执行。

   ```csharp
   button.Click += async (sender, e) =>
   {
       await LongRunningOperationAsync();
       // 异步操作完成后的操作
   };
   ```

4. **异步并行编程：** 使用 `Task.WhenAll` 或 `Task.WhenAny` 方法可以同时处理多个异步任务。

   ```csharp
   Task<int> task1 = LongRunningOperationAsync();
   Task<int> task2 = LongRunningOperationAsync();

   await Task.WhenAll(task1, task2);  // 同时等待两个任务完成

   int result1 = task1.Result;
   int result2 = task2.Result;
   ```

5. **取消异步操作：** 在异步操作执行期间，可以使用 `CancellationToken` 来取消操作，以便资源得到及时释放。

   ```csharp
   private CancellationTokenSource cancellationTokenSource;
   
   public void StartLongRunningOperation()
   {
       cancellationTokenSource = new CancellationTokenSource();
       var token = cancellationTokenSource.Token;
   
       Task.Run(async () =>
       {
           await LongRunningOperationAsync(token);
       });
   }
   
   public void StopLongRunningOperation()
   {
       cancellationTokenSource.Cancel();
   }
   ```

   在取消操作时，可以使用 `cancellationTokenSource.Cancel()` 方法发送取消信号，异步操作中需要检查 `token.IsCancellationRequested` 属性来判断是否取消。

这些是 C# 中异步操作的一些关键概念和用法。使用异步操作可以提高应用程序的性能和响应性，避免阻塞主线程。

希望这个详解对你有帮助！如果你还有其他问题，请随时提问。











## JSON格式

在C#中，JSON（JavaScript Object Notation）是一种常用的数据交换格式。它基于键值对的方式组织数据，易于阅读和编写，并且可以在不同的编程语言中进行解析和生成。

JSON文件的格式包含以下几个主要概念和语法规则：

1. 键值对（Key-Value Pairs）：JSON文件中的数据由一系列键值对组成，键和值之间使用冒号分隔。例如：
   ```json
   {
       "name": "John",
       "age": 25,
       "city": "New York"
   }
   ```

2. 数组（Arrays）：JSON中的值也可以是数组，使用方括号将多个值包围起来，并使用逗号分隔。例如：
   ```json
   {
       "fruits": ["apple", "banana", "orange"]
   }
   ```

3. 对象（Objects）：JSON中的值也可以是对象，对象在键值对的值部分使用花括号包围起来。例如：
   ```
   {
       "person": {
           "name": "John",
           "age": 25,
           "city": "New York"
       }
   }
   ```

JSON文件在C#中常用于以下场景：

1. 数据交换：JSON文件可以作为不同系统或模块之间传递数据的通用格式。通过将数据序列化为JSON格式，发送方可以将数据发送给接收方，接收方可以解析JSON文件并将其还原为对象或数据结构进行处理。

2. 配置文件：JSON文件可以作为应用程序的配置文件，用于存储和读取配置信息。应用程序可以将配置信息存储为JSON文件，并在启动时读取并解析该文件，从而获取所需的配置项。

3. 数据存储：JSON文件可以用于将数据持久化到磁盘或数据库中。应用程序可以将对象或数据结构序列化为JSON格式，并将其存储为文件或将其作为文本存储在数据库中。

在C#中，可以使用Json.NET库（也称为Newtonsoft.Json）来处理JSON文件。该库提供了丰富的API，可以轻松地将对象序列化为JSON格式，或将JSON数据解析为对象。你可以通过NuGet包管理器将Json.NET添加到C#项目中。

以下是一个使用Json.NET库读取和写入JSON文件的示例：

```csharp
using Newtonsoft.Json;
using System.IO;

// 读取JSON文件
string json = File.ReadAllText("data.json");
var data = JsonConvert.DeserializeObject<Data>(json);

// 将对象写入JSON文件
var newData = new Data { Name = "John", Age = 25 };
string newJson = JsonConvert.SerializeObject(newData);
File.WriteAllText("newData.json", newJson);

// 数据对象
class Data
{
    public string Name { get; set; }
    public int Age { get; set; }
}
```
以上示例演示了如何将JSON文件中的数据读取到对象中，

以及如何将对象序列化为JSON并写入到文件中。





你可以在 C# 中使用类来描述这个 JSON 数据。以下是一个示例类的定义，它与给定的 JSON 数据相匹配：

```csharp
using System.Collections.Generic;

public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
    public bool IsStudent { get; set; }
    public List<int> Grades { get; set; }
    public Address Address { get; set; }
    public List<string> Languages { get; set; }
}

public class Address
{
    public string Street { get; set; }
    public string City { get; set; }
}
```

在这个示例中，我们创建了两个类：`Person` 和 `Address`。

`Person` 类有以下属性：

- `Name`：用于存储姓名的字符串属性。
- `Age`：用于存储年龄的整数属性。
- `IsStudent`：用于存储是否为学生的布尔属性。
- `Grades`：用于存储成绩的整数列表属性。
- `Address`：用于存储地址的 `Address` 类对象属性。
- `Languages`：用于存储语言列表的字符串列表属性。

`Address` 类有以下属性：

- `Street`：用于存储街道的字符串属性。
- `City`：用于存储城市的字符串属性。

你可以使用这些类创建对象来表示给定的 JSON 数据，例如：

```csharp
Person person = new Person
{
    Name = "John",
    Age = 25,
    IsStudent = true,
    Grades = new List<int> { 95, 88, 92 },
    Address = new Address
    {
        Street = "123 Main St",
        City = "New York"
    },
    Languages = new List<string> { "English", "Spanish", "French" }
};
```

这样，你就可以在 C# 中以对象的形式方便地处理和操作 JSON 数据。

希望这个示例对你有帮助！如果你还有其他问题，请随时提问。











## 命令

在C#中，命令（Command）是一种常用的设计模式，用于将操作封装为独立的对象，以实现松耦合和可重用性。使用命令模式可以将操作的请求者和执行者解耦，并使其能够灵活地切换和组合不同的操作。

在C#中，可以通过以下几个步骤来创建和使用命令：

1. 创建命令接口：定义一个接口，其中包含一个执行（Execute）方法，用于执行具体的操作。

```csharp
public interface ICommand
{
    void Execute();
}
```

2. 实现具体命令类：根据具体的操作，创建实现命令接口的具体命令类，并在Execute方法中实现相应的操作。

```csharp
public class ConcreteCommand : ICommand
{
    private Receiver _receiver;

    public ConcreteCommand(Receiver receiver)
    {
        _receiver = receiver;
    }

    public void Execute()
    {
        _receiver.Action();
    }
}
```

3. 创建命令请求者（Invoker）：创建一个命令请求者，它负责存储和触发具体命令的执行。

```csharp
public class Invoker
{
    private ICommand _command;

    public void SetCommand(ICommand command)
    {
        _command = command;
    }

    public void ExecuteCommand()
    {
        _command?.Execute();
    }
}
```

4. 创建命令接收者（Receiver）：接收者是实际执行操作的对象。

```csharp
public class Receiver
{
    public void Action()
    {
        Console.WriteLine("Performing command action");
    }
}
```

使用命令的示例代码：

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        Receiver receiver = new Receiver();
        ICommand command = new ConcreteCommand(receiver);
        
        Invoker invoker = new Invoker();
        invoker.SetCommand(command);
        
        invoker.ExecuteCommand();
        
        Console.ReadLine();
    }
}
```

在上述示例代码中，我们首先创建了一个具体命令类ConcreteCommand，它接收一个命令接收者Receiver作为构造函数参数，并调用Receiver的Action方法来执行具体的操作。

然后，我们创建了一个命令请求者Invoker，该请求者可以存储具体命令，并通过调用ExecuteCommand方法来触发命令的执行。

在Main方法中，我们创建了Receiver、ConcreteCommand和Invoker的实例，并将ConcreteCommand设置为Invoker的命令。最后，我们通过调用Invoker的ExecuteCommand方法来执行该命令。

通过使用命令模式，我们可以实现请求者和执行者之间的解耦，并可以轻松地添加新的命令和请求者。此外，命令模式还支持撤销和重做操作，以及对命令进行扩展和组合等功能。





## 多线程并发

[C# 多线程处理_c#多线程并发处理方式_youandme520的博客-CSDN博客](https://blog.csdn.net/youandme520/article/details/103532369)





### BeginInvoke

`Application.Current.Dispatcher.BeginInvoke` 方法将后续的代码调度到 UI 线程上执行，以确保在正确的线程上显示消息对话框。使用匿名委托 `(Action)delegate () { ... }` 来指定将在 UI 线程上执行的操作。



### Invoke

```C#
 //这里是在非UI线程上执行，
            //用于将接收到的消息添加到名为`messageListBox`的列表框(UI元素)
            // 
            // 使用Dispatcher.Invoke()方法将操作推送到UI线程上执行
            // 确保该操作在UI线程上执行，以避免线程间的冲突和异常
            Application.Current.Dispatcher.Invoke(() =>
            {
                //
                messageListBox.Items.Add(message);
            });
```



`BeginInvoke` 和 `Invoke` 是用于在跨线程操作时与 UI 线程进行交互的方法。

`BeginInvoke` 方法是异步的，它会将委托添加到 UI 线程的消息队列中，并在稍后的时间执行。它会立即返回，允许调用的线程继续执行其他任务，而不需要等待 UI 线程中的操作完成。

`Invoke` 方法是同步的，它会阻塞调用的线程，直到 UI 线程执行完成。调用 `Invoke` 方法后，它会等待 UI 线程执行委托中的操作，然后返回结果。这意味着调用 `Invoke` 时，执行顺序会被阻塞，直到 UI 线程处理完委托中的操作。

一般来说，如果您只是需要向 UI 线程发送操作并不需要等待结果，可以使用 `BeginInvoke`。而如果您需要在执行操作后获取结果或必须等待操作完成后继续执行其他任务，您可以使用 `Invoke`。













## DataSet

在C#中，DataSet是一个包含数据表的内存中数据表示形式。它是System.Data命名空间中的一个类，用于在本地存储和处理数据。

DataSet可以包含一个或多个数据表，每个数据表由行和列组成。它提供了许多方法和属性，用于管理和操作数据表，如添加数据行、删除数据行、筛选数据、排序数据等。

下面是一个使用DataSet的简单示例：

```csharp
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // 创建一个DataSet对象
        DataSet dataSet = new DataSet();

        // 创建一个数据表
        DataTable table = new DataTable("Customers");
        
        // 定义数据列
        DataColumn column1 = new DataColumn("CustomerID", typeof(string));
        DataColumn column2 = new DataColumn("Name", typeof(string));
        DataColumn column3 = new DataColumn("Age", typeof(int));
        
        // 将数据列添加到数据表中
        table.Columns.Add(column1);
        table.Columns.Add(column2);
        table.Columns.Add(column3);

        // 创建一行数据
        DataRow row = table.NewRow();
        row["CustomerID"] = "001";
        row["Name"] = "John";
        row["Age"] = 30;
        
        // 将数据行添加到数据表中
        table.Rows.Add(row);

        // 将数据表添加到DataSet中
        dataSet.Tables.Add(table);
        
        // 打印DataSet中的数据
        foreach (DataRow dataRow in dataSet.Tables["Customers"].Rows)
        {
            Console.WriteLine($"CustomerID: {dataRow["CustomerID"]}, Name: {dataRow["Name"]}, Age: {dataRow["Age"]}");
        }
    }
}
```

上述示例创建了一个包含一个数据表的DataSet对象，数据表名为"Customers"。然后，添加了一行数据并将其打印出来。

DataSet提供了许多其他功能，如数据关系的建立、数据表之间的关联、数据的持久化（通过序列化和反序列化）等。可以根据具体需求使用DataSet来处理和操作数据。



LINQ

LINQ（Language Integrated Query）是C#中的一种查询语言，它提供了一种强大而灵活的方式来查询数据。LINQ可以与各种数据源一起使用，如集合、数组、XML文档、数据库等。以下是C#中LINQ的详细解释：

1. 查询表达式： LINQ使用一种类似于SQL的查询语法，称为查询表达式。它允许在C#代码中编写直观的查询，而无需编写显式的循环。查询表达式使用类似于`from`、`where`、`select`等关键字来构建查询。

   ```csharp
   // 查询表达式示例
   var query = from student in students
               where student.Age > 18
               select student.Name;
   ```
   
2. 扩展方法： LINQ还提供了一组扩展方法，它们扩展了集合类和其他类的功能，使其能够进行查询操作。这些扩展方法定义在名为`System.Linq`的命名空间中。

   ```csharp
   // 扩展方法示例
   var query = students.Where(student => student.Age > 18)
                      .Select(student => student.Name);
   ```

   上述示例中的`Where`和`Select`方法是LINQ提供的扩展方法，`Where`用于过滤满足指定条件的元素，而`Select`用于选择指定的元素。

3. 查询运算符： LINQ提供了一系列查询运算符，用于对数据进行操作和过滤，如过滤、排序、投影、分组等。

   - `Where`：用于筛选满足指定条件的元素。
   - `OrderBy`：用于对元素进行升序排序。
   - `OrderByDescending`：用于对元素进行降序排序。
   - `Select`：用于选择指定的元素。
   - `GroupBy`：用于将元素按照指定的键进行分组。
   - 等等。

   ```csharp
   // 查询运算符示例
   var query = students.Where(student => student.Age > 18)
                      .OrderBy(student => student.Name)
                      .Select(student => student.Name);
   ```

4. 匿名类型： 在LINQ中，可以使用匿名类型表示查询结果中的临时数据。匿名类型可以在查询表达式或扩展方法中使用。

   ```csharp
   // 匿名类型示例
   var query = from student in students
               where student.Age > 18
               select new { student.Name, student.Age };
   ```

   上述示例中，查询结果是一个匿名类型的集合，每个匿名类型对象包含学生的姓名和年龄。

5. 延迟执行： LINQ的查询是延迟执行的，也就是说查询不会立即执行，而是在使用查询结果时才会触发执行。

   ```csharp
   // 延迟执行示例
   var query = from student in students
               where student.Age > 18
               select student.Name;
               
   // 在使用查询结果时触发执行
   foreach (var name in query)
   {
       Console.WriteLine(name);
   }
   ```

   上述示例中，查询在`foreach`循环中使用时才会执行，这样可以避免在查询不需要的情况下浪费资源。

这是对C#中LINQ的一些详细解释，希望对你有所帮助。请注意，以上只是LINQ的基本概念和用法，LINQ还有更多的特性和用法，可以根据具体需求进行深入学习和探索。









## 依赖注入



底层的哈希表

[详解C#中的依赖注入和IoC容器_C#/.NET开发-小镜子 (xujingzi.com)](http://www.xujingzi.com/nav/net/96899.html)



[C#依赖注入_c# 依赖注入_星辉Johnson的博客-CSDN博客](https://blog.csdn.net/qq_18145031/article/details/83181937)

### GPT

依赖注入（Dependency Injection，简称DI）是一种设计模式，它允许对象在创建时通过构造函数，属性或方法参数的方式，将其依赖的对象（依赖项）传递给它，而不是由对象自己创建。

在C#中，依赖注入是实现松耦合和可测试性的重要技术。通过使用依赖注入，可以使代码更易于理解、测试和维护。

下面是一个简单的示例，展示了如何使用依赖注入：

```csharp
using System;

// 定义一个服务接口
public interface IHelloService
{
    void SayHello();
}

// 实现服务接口
public class HelloService1 : IHelloService
{
    public void SayHello()
    {
        Console.WriteLine("Hello, World!");
    }
}





// 客户端类，依赖于IHelloService接口
public class Client
{
    private IHelloService _helloService;

    // 通过构造函数注入依赖项
    public Client(IHelloService helloService)
    {
        _helloService = helloService;
    }

    public void Greet()
    {
        _helloService.SayHello();
    }
}

// 程序入口
class Program
{
    static void Main()
    {
        // 创建服务实例
        IHelloService helloService = new HelloService1();

        // 创建客户端实例，注入依赖项
        Client client = new Client(helloService2);

        // 使用客户端
        client.Greet();
    }
}
```

在上述示例中，首先定义了一个服务接口`IHelloService`和其实现类`HelloService`。然后，客户端类`Client`通过构造函数注入`IHelloService`接口的实例。

在程序入口的`Main`方法中，我们创建了`HelloService`的实例，并将其作为参数传递给`Client`对象。最后，通过调用`client.Greet()`方法，客户端使用注入的`IHelloService`实例调用了`SayHello()`方法。

依赖注入有助于解耦依赖关系，并便于在测试时模拟依赖项。在大型的应用程序中，通常使用IoC容器（如Microsoft.Extensions.DependencyInjection）来管理对象的创建和依赖项的注入。

使用IoC容器时，我们可以**在配置文件或代码中注册服务和对象的依赖关系**。然后，**IoC容器将自动解析依赖关系并为我们创建对象**。

详解如下

在C#中，使用依赖注入(Dependency Injection，DI)可以帮助解耦和组织代码，并提高代码的可测试性和可维护性。在.NET Core中，依赖注入有一个内置的容器，可通过IServiceCollection和IServiceProvider进行配置和使用。

依赖注入的原理是将对象的创建和依赖的解析工作委托给容器来完成。具体步骤如下：

1. 首先，需要定义服务接口和实现类。接口定义了服务的合同，实现类提供了具体的实现逻辑。

```csharp
public interface IMyService
{
    void DoSomething();
}

public class MyService : IMyService
{
    public void DoSomething()
    {
        // 实现逻辑
    }
}
```

2. 在Startup类的ConfigureServices方法中，将服务注册到依赖注入容器中。

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddTransient<IMyService, MyService>();
}
```

上述代码使用`**AddTransient**`方法将IMyService接口注册为MyService实现类的一个瞬时（Transient）服务。还可以使用`AddScoped`（作用域服务）或`AddSingleton`（单例服务）等其他方法进行注册。

3. 在需要使用服务的地方，通过构造函数或属性注入方式获取服务的实例。

```csharp
public class MyClass
{
    private readonly IMyService _myService;

    public MyClass(IMyService myService)
    {
        _myService = myService;
    }

    public void DoSomething()
    {
        _myService.DoSomething();
    }
}
```

通过构造函数注入的方式，容器会自动解析依赖并提供实例。

使用依赖注入的好处包括：

1. 解耦：依赖注入将服务的创建和组装工作委托给容器，降低了类之间的直接依赖关系，提高了代码的可扩展性和灵活性。

2. 可测试性：通过依赖注入，可以轻松地使用模拟对象或虚拟实现进行单元测试，减少了对外部依赖的耦合，提高了测试的可信度和可维护性。

3. 可替换性：依赖注入使得可以轻松替换服务的实现类，例如在不同环境中使用不同的实现。

4. 可维护性：通过依赖注入，代码结构更清晰，且易于扩展和修改，使得代码维护更加简单和可靠。

总之，依赖注入是一个强大的设计模式和编程范式，可以帮助提高代码的质量、可测试性和可维护性，是现代软件开发中广泛使用的技术和理念之一。



依赖注入（Dependency Injection，简称DI）是一种软件设计模式，它通过将组件的依赖关系从组件内部移出，由外部容器负责创建和提供这些依赖项。依赖注入的目的是实现组件之间的松耦合，提高代码的可测试性、可维护性和可扩展性。

在C#中，依赖注入广泛应用于各种类型的项目，特别是在大型和复杂的应用程序中。下面介绍一些依赖注入的概念和应用：

1. 依赖关系（Dependency）：一个组件可能会依赖于其他组件或服务来完成特定的功能。这些依赖关系可以是其他类、接口、配置信息、数据库连接等。

2. 依赖注入容器（DI Container）：依赖注入容器负责管理组件之间的依赖关系，并在需要时创建和提供这些依赖项。容器通过反射或配置文件等方式，将依赖关系与组件关联起来。

3. 注入方式（Injection Types）：依赖注入可以通过构造函数注入、属性注入或方法注入等方式进行。构造函数注入是最常见的方式，通过在组件的构造函数中声明它所依赖的类型，容器在创建组件实例时会自动解析并注入这些依赖项。

4. 生命周期管理（Lifetime Management）：依赖注入容器可以管理组件的生命周期，例如单例模式、每次请求一个新实例等。通过合理管理组件的生命周期，可以确保依赖项的正确创建和释放，避免资源泄漏或内存溢出等问题。

5. 自动化配置（Convention-based Configuration）：依赖注入容器可以通过约定和规则自动配置组件和依赖关系，减少手动配置的工作量。例如，容器可以根据命名规则自动查找和注册符合特定接口的实现类。

6. 单元测试和模拟对象（Unit Testing and Mocking）：依赖注入极大地简化了单元测试和模拟对象的创建。通过将组件的依赖关系外部化，我们可以轻松地替换依赖项为模拟对象，以进行单元测试和隔离测试。

使用依赖注入可以提高代码的可维护性和可测试性，降低代码的耦合性，促进代码的重用和扩展性。它将组件的依赖关系从组件内部分离出来，使得整个系统更加灵活和可配置。

常用的依赖注入容器包括 Autofac、Unity、Ninject、Simple Injector 等。你可以根据项目的需求和个人喜好选择适合的依赖注入容器，并按照它们的文档和示例进行使用。



容器使用参考如下代码

```c#
 public class BaseService<T> : IBaseService<T> where T : class, IHasId, new()
    {

        private IGenericService<T> genericService;
        public BaseService()
        {
            IHost host = Host.CreateDefaultBuilder()
                      .ConfigureServices((context, services) =>
                      {
                          services.AddTransient<GenericService<T>>();
                          services.AddTransient<IGenericRepository<T>, GenericRepository<T>>();
                      })
                      .Build();

            genericService = host.Services.GetRequiredService<GenericService<T>>();

        }

        public IGenericService<T> GetGenericService()
        {
            return genericService;
        }
    }
```



特别注意

这段代码中的两次注册，使用了不同的方式来实现依赖注入（Dependency Injection）。让我来解释一下它们的不同之处：

1. 第一次注册：
   ```c#
   services.AddTransient<GenericService<T>>();
   ```
   这种方式是使用类型本身的方式进行注册。它将 `GenericService<T>` 类型注册为服务，以便以后在代码中使用依赖注入来获取该类型的实例。此注册方式适用于需要在每次请求时都创建一个新的实例的情况，例如无状态的服务。

2. 第二次注册：
   ```c#
   services.AddTransient<IGenericRepository<T>, GenericRepository<T>>();
   ```
   这种方式是使用接口和实现类型的方式进行注册。它将 `IGenericRepository<T>` 接口和 `GenericRepository<T>` 实现类型进行关联，以便在代码中使用依赖注入来获取 `IGenericRepository<T>` 的实例。此方法主要用于解耦和实现依赖倒转原则，让代码更灵活、可测试。

两种注册方式的选择取决于具体的需求和设计决策。你可以根据实际情况选择合适的方式来注册你的服务。





### 个人理解

依赖注入的方式不难理解

关键是对容器的理解，

注册，其实就是在容器中，建立接口与继承者的关系，目的在于借助容器帮助你依赖注入

这话看着很迷，  但是用着，就顿悟了

它的底层是用哈希表实现的检索，

那么在容器中，通过反射和传参，最终制造一个你需要的实例对象

 

我这里说的比较抽象

参考下图的简单容器的实现逻辑，

 _registrations  是哈希表的实例对象

通过反射制造你想要的对象

注意，要注册













## 动态代理

[C#动态代理 (bluesd7.com)](http://bluesd7.com/蓝影闪电的随笔/ContentId/120/C)



在C#中，动态代理是一种代理设计模式的实现方式，它允许在运行时创建一个代理对象，并将所有对该对象的方法调用转发给被代理的实际对象。动态代理使我们能够以统一的方式对不同的对象进行代理，而无需针对每个对象手动创建代理类。

C#中的动态代理一般通过以下两种方式来实现：

1. 使用`RealProxy`类：`.NET Remoting`中的`RealProxy`类提供了一种动态创建代理的方式。通过创建一个自定义的`RealProxy`子类，并实现其`Invoke`方法，可以在运行时拦截并处理对代理对象的调用。然后，使用`CreateProxy`方法创建代理对象。

2. 使用`DynamicProxy`库：`DynamicProxy`是由`Castle Project`提供的一个第三方库，用于动态创建代理类。该库提供了一个`ProxyGenerator`类，可以通过创建一个接口或基类的代理，使方法调用被重定向到代理类中的自定义调用处理程序。这个库在运行时创建代理类，基于已有的接口或基类进行代理。

动态代理在实现AOP（面向切面编程）的时候非常有用，可以在不修改原始类的情况下，通过代理对象来添加额外的功能、日志、事务管理等。同时，动态代理也在一些ORM框架和测试框架中得到广泛的应用。

下面是一个简单的示例代码，演示如何使用`DynamicProxy`库来创建动态代理类：

首先，需要安装`Castle.Core`和`Castle.DynamicProxy`这两个NuGet包。

```csharp
using Castle.DynamicProxy;
using System;

// 定义一个接口
public interface ICalculator
{
    int Add(int a, int b);
}

// 实现接口的类
public class Calculator : ICalculator
{
    public int Add(int a, int b)
    {
        return a + b;
    }
}

// 定义一个自定义的调用处理程序
public class CustomInterceptor : IInterceptor
{
    public void Intercept(IInvocation invocation)
    {
        Console.WriteLine("Before method call");
        invocation.Proceed(); // 调用被代理对象的方法
        Console.WriteLine("After method call");
    }
}

class Program
{
    static void Main(string[] args)
    {
        // 创建代理生成器
        ProxyGenerator generator = new ProxyGenerator();

        // 创建被代理对象
        Calculator calculator = new Calculator();

        // 创建代理，并指定调用处理程序
        ICalculator proxy = generator.CreateInterfaceProxyWithTargetInterface<ICalculator>(calculator, new CustomInterceptor());

        // 调用代理对象的方法
        int result = proxy.Add(3, 4);

        Console.WriteLine("Result: " + result);
    }
}
```

在这个示例中，我们首先定义了一个名为`ICalculator`的接口，包含了一个`Add`方法。然后，我们实现了这个接口的类`Calculator`。

接下来，我们定义了一个名为`CustomInterceptor`的自定义调用处理程序，它实现了`IInterceptor`接口。在`Intercept`方法中，我们在方法调用前后输出一些信息。

在`Main`方法中，我们首先创建一个`ProxyGenerator`对象。然后，我们创建了一个`Calculator`对象作为被代理对象。接着，通过调用`ProxyGenerator`的`CreateInterfaceProxyWithTargetInterface`方法，我们使用被代理对象和`CustomInterceptor`作为参数来创建代理对象。

最后，我们调用代理对象的`Add`方法，并输出结果。在调用过程中，会先执行`CustomInterceptor`中的`Intercept`方法，输出预设的信息，然后再调用实际的方法。

这样，我们就实现了一个简单的动态代理示例，通过添加自定义的调用处理程序，在调用前后进行额外的操作。请注意，以上示例是使用`DynamicProxy`库来实现动态代理的一种方式，`DynamicProxy`库还支持其他更高级的功能，例如拦截特定的方法、获取方法参数和返回值等。





## Mutex互斥锁

在C#中，`Mutex`是一种互斥锁（Mutual Exclusion Lock），它用于实现多线程之间的互斥访问。`Mutex`类提供了一种同步机制，确保只有一个线程能够同时访问受保护的资源，从而避免竞争条件和数据损坏。

在使用`Mutex`时，你可以创建一个新的`Mutex`对象，并使用它来控制多个线程的访问。下面是一个简单的示例：

```csharp
using System;
using System.Threading;

class Program
{
    static Mutex mutex = new Mutex();

    static void Main()
    {
        // 创建两个线程
        Thread thread1 = new Thread(DoWork);
        Thread thread2 = new Thread(DoWork);

        // 启动线程
        thread1.Start();
        thread2.Start();

        // 等待线程完成
        thread1.Join();
        thread2.Join();
    }

    static void DoWork()
    {
        // 请求互斥锁
        mutex.WaitOne();

        try
        {
            // 在临界区内访问受保护的资源
            Console.WriteLine($"Thread {Thread.CurrentThread.ManagedThreadId} is accessing the protected resource.");
            Thread.Sleep(1000);
        }
        finally
        {
            // 释放互斥锁
            mutex.ReleaseMutex();
        }
    }
}
```

在上述示例中，我们创建了一个共享的`Mutex`对象，并在两个线程中使用它来控制对受保护资源的访问。

在`DoWork`方法中，线程首先通过调用`mutex.WaitOne()`请求互斥锁，以确保只有一个线程能够进入临界区代码。然后，在临界区内，线程访问受保护的资源，并在一段时间后释放互斥锁，以允许其他线程进入临界区。

使用`Mutex`可以很好地确保多线程环境下的互斥访问，并避免出现竞争条件和数据不一致的问题。







## XDocument与XElement

### XDocument

XDocument是C#中用于处理XML文档的类，它位于System.Xml.Linq命名空间中。XDocument类提供了一系列方法和属性，用于读取、创建、修改和写入XML文档。

以下是一些XDocument类的常用方法和属性：

1. 加载XML文档：

- `XDocument.Load(string uri)`：从指定的文件或URL加载XML文档。
- `XDocument.Parse(string xml)`：从字符串中解析XML文档。

2. 创建XML文档：

- `XDocument()`：创建一个新的空XML文档对象。
- `XDocument(XDeclaration declaration, params object[] content)`：使用指定的声明和内容创建一个新的XML文档。

3. 获取XML文档的根元素：

- `Root`属性：获取XML文档的根元素（XElement对象）。

4. 查询XML元素/节点：

- `Descendants()`：返回指定名称的所有后代元素。
- `Elements()`：返回指定名称的直接子元素。
- `Attributes()`：返回指定名称的元素的属性。

5. 修改XML文档：

- `Add(object content)`：向XML文档中添加元素、注释、文本等内容。
- `Remove()`：从XML文档中移除指定的元素或节点。

6. 保存XML文档：

- `Save(string fileName)`：将XML文档保存到指定的文件中。

这只是XDocument类的一部分功能，还有其他更多的方法和属性可供使用。使用XDocument，您可以轻松地读取和处理XML文档的内容，进行查询、修改和保存操作。



### XElement

在C#中，XElement是表示XML元素的类，它位于System.Xml.Linq命名空间中。XElement是使用LINQ to XML技术来处理XML文档的主要类之一。XElement类提供了一系列方法和属性，用于读取、创建、修改和操作XML元素。

以下是一些常用的XElement类方法和属性：

1. 获取元素的属性：

- `Attribute(XName name)`：检索给定名称的属性。
- `Attributes()`：返回元素的所有属性。
- `SetAttributeValue(XName name, object value)`：设置或添加给定名称的属性值。
- `RemoveAttributes()`：从元素中移除所有属性。

2. 获取元素的子元素：

- `Element(XName name)`：检索给定名称的第一个子元素。
- `Elements()`：返回元素的所有子元素。

3. 获取元素的值和文本：

- `Value`属性：获取或设置元素的文本值。
- `ToString()`：将元素及其内容转换为字符串表示。

4. 修改元素及其内容：

- `Add(object content)`：向元素中添加元素、注释、文本等内容。
- `Remove()`：从父元素中移除该元素。

5. 查询元素或节点：

- `Descendants()`：返回指定名称的所有后代元素。
- `Ancestors()`：返回指定名称的所有祖先元素。

6. 获取元素的名称和命名空间：

- `Name`属性：获取或设置元素的名称（XName对象）。
- `Name.Namespace`：获取元素的命名空间。

这只是XElement类的一部分功能，还有其他更多的方法和属性可供使用。使用XElement，您可以轻松地读取和处理XML元素的属性、值、子元素等。



### 二者区别

XDocument和XElement是C#中用于处理XML文档的两个类，它们有以下区别：

1. 功能不同：
- XDocument类代表整个XML文档，包括XML文档的声明和根元素，它提供了加载、创建、修改和保存整个XML文档的功能。
- XElement类代表XML文档中的一个元素，它提供了访问和操作单个元素的属性、子元素和值的功能。

2. 级别不同：
- XDocument位于XML文档的最顶层，可以包含XML文档的声明和根元素，而且还可以包含注释、处理指令和其他元素。
- XElement是XML文档中的一个元素，它可以包含属性、子元素和文本值。

3. 使用方式不同：
- XDocument通常用于加载、创建和保存整个XML文档。您可以使用XDocument.Load()来加载XML文件，使用XDocument.Parse()来解析字符串创建XML文档，使用XDocument.Save()来保存XML文档到文件。
- XElement通常用于查询和修改单个元素或特定元素的属性、子元素和值。您可以使用XElement的方法和属性来获取、修改和删除元素的内容。

一般来说，您可以使用XDocument来操作整个XML文档，而使用XElement来操作单个元素。根据您的具体需求，可以选择使用适合的类来处理XML文档。





## 常用接口说明

### ICloneable

在C#中，ICloneable是一个接口，用于实现对象的复制。它定义了一个方法Clone，该方法允许创建当前对象的浅拷贝（仅复制对象的字段或属性的值，而不复制引用类型的实际对象）。

以下是ICloneable接口的定义：

```csharp
public interface ICloneable
{
    object Clone();
}
```

要实现ICloneable接口，需要在类上实现Clone方法，并且返回该类的对象。

例如，假设我们有一个名为Person的类，它实现了ICloneable接口：

```csharp
public class Person : ICloneable
{
    public string Name { get; set; }
    public int Age { get; set; }

    public object Clone()
    {
        return this.MemberwiseClone();
    }
}
```

在上面的示例中，Person类实现了ICloneable接口，并在Clone方法中使用了  MemberwiseClone方法  返回当前对象的浅拷贝。

使用ICloneable接口时，可以通过调用Clone方法来创建一个对象的副本，如下所示：

```csharp
Person person1 = new Person();
person1.Name = "John";
person1.Age = 25;

Person person2 = (Person)person1.Clone();
```

在上面的示例中，我们通过调用person1的Clone方法创建了person2对象，person2是person1的一个浅拷贝。

需要注意的是，ICloneable接口默认实现是浅拷贝，即对于引用类型的成员，仅复制引用而不复制实际对象。如果需要深拷贝，即将引用类型的成员也进行复制，**需要在Clone方法中编写自定义的深拷贝逻辑**。







在实参中传递请求头时，可以通过创建一个`HttpRequestMessage`对象，设置相应的请求头，然后使用该对象作为`client.SendAsync()`方法的参数。

下面是修改后的代码示例：

```csharp
public async Task<string> Post(string url, HttpContent content, Dictionary<string, string> headers)
{
    var request = new HttpRequestMessage(HttpMethod.Post, url);
    request.Content = content;

    foreach (var header in headers)
    {
        request.Headers.Add(header.Key, header.Value);
    }

    HttpResponseMessage response = await client.SendAsync(request);

    if (response.IsSuccessStatusCode)
    {
        string responseBody = await response.Content.ReadAsStringAsync();
        return responseBody;
    }
    else
    {
        throw new Exception($"HTTP POST request failed with status code: {response.StatusCode}");
    }
}
```

在调用`Post`方法时，可以通过将请求头信息以字典的形式传递给`headers`参数。每个字典项中的键表示请求头的名称，值表示请求头的值。

示例调用示意：
```csharp
Dictionary<string, string> headers = new Dictionary<string, string>();
headers.Add("Content-Type", "application/json");
headers.Add("Authorization", "Bearer <token>");

string responseBody = await Post(url, content, headers);
```

在以上示例中，设置了`Content-Type`和`Authorization`两个请求头。你可以根据实际需要设置所需的请求头信息。











要使用表单上传参数，可以使用`MultipartFormDataContent`类来创建`HttpContent`对象，并添加键值对参数到表单中。

以下是优化的代码示例：

```csharp
public async Task<string> Post(string url, Dictionary<string, string> formData)
{
    var formContent = new MultipartFormDataContent();

    foreach (var kvp in formData)
    {
        formContent.Add(new StringContent(kvp.Value), kvp.Key);
    }

    HttpResponseMessage response = await client.PostAsync(url, formContent);

    if (response.IsSuccessStatusCode)
    {
        string responseBody = await response.Content.ReadAsStringAsync();
        return responseBody;
    }
    else
    {
        throw new Exception($"HTTP POST request failed with status code: {response.StatusCode}");
    }
}
```

在调用`Post`方法时，可以将要上传的参数以字典的形式传递给`formData`参数。每个字典项中的键表示参数的名称，值表示参数的值。

示例调用示意：
```csharp
Dictionary<string, string> formData = new Dictionary<string, string>();
formData.Add("username", "testuser");
formData.Add("password", "123456");

string responseBody = await Post(url, formData);
```

在以上示例中，添加了两个表单参数：`username`和`password`。你可以根据实际需要添加更多的表单参数。







表单可以添加对象类型，但是在使用`MultipartFormDataContent`来添加对象时，需要将对象序列化为字符串。常见的序列化方式包括 JSON 格式和表单 URL 编码格式。

以下是更改后的代码示例，可以添加对象类型的参数到表单中：

```csharp
public async Task<string> Post(string url, Dictionary<string, object> formData)
{
    var formContent = new MultipartFormDataContent();

    foreach (var kvp in formData)
    {
        if (kvp.Value is string)
        {
            // 字符串类型直接添加到表单
            formContent.Add(new StringContent(kvp.Value.ToString()), kvp.Key);
        }
        else
        {
            // 对象类型需要序列化为字符串后再添加到表单
            string serializedValue = JsonConvert.SerializeObject(kvp.Value);
            formContent.Add(new StringContent(serializedValue), kvp.Key);
        }
    }

    HttpResponseMessage response = await client.PostAsync(url, formContent);

    if (response.IsSuccessStatusCode)
    {
        string responseBody = await response.Content.ReadAsStringAsync();
        return responseBody;
    }
    else
    {
        throw new Exception($"HTTP POST request failed with status code: {response.StatusCode}");
    }
}
```

在调用`Post`方法时，可以将要上传的参数以字典的形式传递给`formData`参数。每个字典项中的键表示参数的名称，值表示参数的值。参数的值可以是任意类型，如果是字符串类型，则直接添加到表单中；如果是对象类型，则会进行序列化为字符串后再添加到表单中。

示例调用示意：
```csharp
Dictionary<string, object> formData = new Dictionary<string, object>();
formData.Add("username", "testuser");
formData.Add("password", "123456");

var authorities = new List<object>
{
    new
    {
        resourceId = "1e0bfebe-d424-11ed-93ed-ac50de9e2239",
        canRead = true,
        canWrite = false,
        canExecute = true
    }
};
formData.Add("authorities", authorities);

string responseBody = await Post(url, formData);
```

在以上示例中，添加了两个普通字符串参数：`username`和`password`，以及一个对象类型参数`authorities`。`authorities`参数被序列化为 JSON 字符串后添加到表单中。







## 常用特性说明

### Description

Description特性是C#提供的一个自定义特性，它可以用于为类、属性、方法等程序元素添加描述信息。Description特性通常用于提供更详细的文档、注释或简单的说明。

以下是Description特性的使用示例：

```csharp
using System;
using System.ComponentModel;

public class MyClass
{
    [Description("这是一个示例属性")]
    public int MyProperty { get; set; }

    [Description("这是一个示例方法")]
    public void MyMethod()
    {
        // 方法实现
    }
}

public class Program
{
    public static void Main()
    {
        var myClass = new MyClass();

        // 获取属性的Description特性值
        DescriptionAttribute propertyDescription = (DescriptionAttribute)Attribute.GetCustomAttribute(typeof(MyClass).GetProperty("MyProperty"), typeof(DescriptionAttribute));
        
        string propertyDescriptionValue = propertyDescription.Description;
        Console.WriteLine(propertyDescriptionValue);

        // 获取方法的Description特性值
        DescriptionAttribute methodDescription = (DescriptionAttribute)Attribute.GetCustomAttribute(typeof(MyClass).GetMethod("MyMethod"), typeof(DescriptionAttribute));
        
        string methodDescriptionValue = methodDescription.Description;
        Console.WriteLine(methodDescriptionValue);
    }
}
```

在上述示例中，我们定义了一个名为MyClass的类，该类具有一个带有Description特性的属性`MyProperty`和一个带有Description特性的方法`MyMethod`。在Main方法中，我们可以使用Attribute.GetCustomAttribute方法来访问这些特性，并获取它们的值。

注意，Description特性本身并不会对程序的逻辑产生任何影响，它仅用于提供描述信息，并且可以在需要时通过反射等方式进行访问。







### DllImport

DllImport是一个用于在C#中导入外部函数的特性。它可以用来调用非托管代码、动态链接库（DLL）中的函数或者由其他编程语言编写的类库。

使用DllImport特性可以告诉编译器去查找和加载指定的DLL，并把函数的调用关联到正确的函数入口点上。

以下是DllImport特性的基本用法：

1. 在函数签名前使用[DllImport("LibraryName.dll")]指定要导入的DLL文件名（**包括文件路径**）
2. 可以使用DllImport的EntryPoint参数来指定函数的入口点，如果不设置，默认使用函数名称。
3. 根据需要，可以使用其他参数，例如 CallingConvention 指定调用约定、CharSet 更改字符集等。

在你给出的代码示例中，DllImport特性被用于导入名为"HMSLaser.dll"的动态链接库，并指定了函数入口点为"HMSSetChangByCard"。这样就能在C#代码中调用该DLL中的函数。







### SugarColumn

```C#
 [SugarColumn(IsPrimaryKey = true)]

IsPrimaryKey 表示是否设置为主键
```

```C#
[SugarColumn(IsNullable = true)]

IsNullable标记可为空
```

```
数据是自增需要加上IsIdentity
```



```
[SugarColumn(IsIgnore =true)] 

表示 ORM 所有操作不处理这列 一般用于数据库没有这一列
```





## Guid

在 C# 中，`Guid` 是一个结构，代表了一个全球唯一标识符（Globally Unique Identifier）。`Guid` 结构在 `System` 命名空间下，它通常用来为应用程序中的对象提供一个唯一的标识符。由于其唯一性质，`Guid`在需要确保对象的独一无二，例如在数据库中作为记录的主键或者在分布式系统中为不同的组件提供一个唯一的标识符时，非常有用。

`Guid` 是一个 128 位整数（16 字节），通常用 32 个十六进制数字表示，并由五组数字组成，格式为 `8-4-4-4-12`，例如 `123e4567-e89b-12d3-a456-426614174000`。

### 创建 Guid

C# 中创建 `Guid` 对象可以通过几种方式：

1. `Guid.NewGuid()`: 创建一个新的、唯一的 Guid。

```csharp
Guid guid = Guid.NewGuid();
Console.WriteLine(guid.ToString());
```

2. 使用 Guid 的构造函数，可以从一个字节数组或者某些特定的字符串格式创建一个 Guid。

```csharp
byte[] bytes = new byte[16];
// 假设 bytes 数组已通过某种方式获取
Guid guidFromBytes = new Guid(bytes);

string guidString = "123e4567-e89b-12d3-a456-426614174000";
Guid guidFromString = new Guid(guidString);
```

3. `Guid.Parse(string)` 和 `Guid.TryParse(string, out Guid)`: 从一个字符串解析出 Guid。

```csharp
string guidString = "123e4567-e89b-12d3-a456-426614174000";
Guid parsedGuid = Guid.Parse(guidString);

Guid tryParsedGuid;
if (Guid.TryParse(guidString, out tryParsedGuid))
{
    // 解析成功
}
```

### Guid 格式

`Guid` 提供了多种格式化选项，可以通过 `ToString` 方法指定：

```csharp
Guid guid = Guid.NewGuid();

// "D" 格式 (默认): 32 位数字，连字符分隔
Console.WriteLine(guid.ToString("D"));

// "N" 格式: 32 位数字，无连字符
Console.WriteLine(guid.ToString("N"));

// "B" 格式: 32 位数字，括在大括号内，有连字符
Console.WriteLine(guid.ToString("B"));

// "P" 格式: 32 位数字，括在圆括号内，有连字符
Console.WriteLine(guid.ToString("P"));

// "X" 格式: 用大括号括起来的四个十六进制值，包含子段
Console.WriteLine(guid.ToString("X"));
```

### 比较 Guid

`Guid` 结构实现了 `IEquatable<Guid>` 接口，所以你可以使用 `Equals` 方法比较两个 `Guid` 对象是否相等。同样，可以使用 `==` 和 `!=` 运算符。

### 注意事项

- 虽然 `Guid` 基本上可以保证是全球唯一的，但技术上它们是使用算法生成的，因此不能保证绝对唯一性。
- 使用 `Guid` 作为数据库表的主键时，需要考虑到 `Guid` 的存储和性能代价，因为其比传统的整数主键大并且可能影响插入性能。

`Guid` 结构是 .NET 为开发者提供的一个强大工具，用于生成和操作唯一标识符。在分布式系统、数据库和需要唯一性的任何场景中，`Guid` 是常见的选择。



由于您提到了要“继续”，我假设您可能对`Guid`的其他方面或高级特性感兴趣，或者想要解决具体问题。以下是一些关于`Guid`更高级一点的话题：

### Guid 版本

`Guid` 有多个版本，它们是使用不同的算法生成的。最常用的是版本 4，它基本上是随机生成的。Guid 的第 13 位（按照传统表示形式）是它的版本号。在 .NET 中，使用 `Guid.NewGuid()` 方法生成的 Guid 是版本 4，它通过随机数生成器来创建。

### Guid 如何生成

在 .NET Core 和 .NET 5+ 中，`Guid` 使用的伪随机数生成器依赖于操作系统提供的机制。Windows 上通常使用 `CoCreateGuid` API，而在 Unix-like 系统上使用 `/dev/urandom`。

### 性能问题

由于 `Guid` 是由 128 位组成，它们会占用比整型更多的空间，并可能导致数据库或其他存储系统的性能问题。此外，在索引时，随机的 `Guid` 值会引起索引碎片和额外的写入负载。在数据库中对 Guid 进行索引时，一个常见的建议是使用顺序 `Guid`（例如 SQL Server 中的 `NEWSEQUENTIALID()` 函数），这样在插入新条目时，索引不会产生太多的随机 I/O。

### Guid 安全性

尽管 `Guid` 通常用于生成狯猾复杂的键值，这意味着它们通常不容易被猜出，但它们不应被视为安全的令牌，因为标准的 `Guid` 算法并不是为了不可预知性而设计的。在需要令牌或键的场景中，应使用专门为安全性设计的算法（例如使用足够长度的随机数，并提供强防护，如使用加密的PRNG）。

### 适用场景

`Guid` 在以下场景下尤为有用：
- 分布式系统：保证即使在不同系统和上下文中也能够生成唯一的标识符。
- 数据库：作为记录的主键，特别是当数据需要跨多个数据库或数据库表分区时。
- 文件名或临时对象：确保不会与现有文件或对象名冲突。

### 示例：在数据库操作中使用 Guid

在使用 Entity Framework (EF) 进行数据库操作时，`Guid` 通常被用作实体的主键：

```csharp
public class User
{
    public Guid Id { get; set; } = Guid.NewGuid();
    public string Name { get; set; }
}

// 在添加新用户到数据库时，每个用户都会被分配一个唯一的 Guid
using (var context = new UserContext())
{
    var newUser = new User { Name = "Alice" };
    context.Users.Add(newUser);
    context.SaveChanges();
}
```

在这个例子中，每创建一个新的 `User` 实例，都会自动为其 `Id` 属性生成一个新的 `Guid`。

如果您有特定的问题或用例，我可以提供更加针对性的指导和示例。请随时提出具体问题！



