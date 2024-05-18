​	



### 顶尖大佬博客

[WPF入门基础教程系列 - 随笔分类 - 痕迹g - 博客园 (cnblogs.com)](https://www.cnblogs.com/zh7791/category/1528742.html)



### WPF方法论

WPF的XAML语言就是用于编写软件的表示层（UI设计）

与WinFrom和Qt不同的是，WPF不是“事件驱动”，它是“数据驱动”，二者正好相反

（内容决定形式）把事件包装在数据关联里

当数据发生变化时，会主动通知界面控件，推动控件展示最新数据，

同时，用户对控件的操会直达数据，似乎控件是**透明的** ，

数据占据主动地位，控件以及控件事件被弱化

（数据驱动程序运行并显示在UI上）





### 一个简单的MVVM设计模式

一个本应该收录于设计模式的内容，只是我个人觉得放在此处更加得体

MVVM模式，与3层架构以及WPF中“ 内容决定形式”的方法论正好不谋而合

以下是补充说明的注意事项，代码注释有写好的详细解释

首先，

```XAML
  xmlns:models="clr-namespace:HHY_WPF_Test.Models" 
  d:DataContext="{d:DesignInstance Type=VM:SampleVM}"
```



这两行代码是在UI层（V层）灯泡自动提示的代码

是用来给出绑定提示的路径（设置后才可找到跳转到定义）



注意，绑定可以绑定UI中控件的属性，亦可以是控件中的命令绑定

对于控件中的命令绑定（例如按键），在XAML代码中按键绑定了VM中的数据实例的命令属性









### WPF 工程文件说明

**1，App.xaml和App.xaml.cs：**
App.xaml是应用程序的入口点，用于定义应用程序的全局资源、样式和事件处理程序等。

​	其中下面这条语句表示，该程序的**默认启动的**入口窗口指向的是哪一个窗口，此处可供需求来设置

```XAML
StartupUri="MainWindow.xaml">
```

告诉编译器把由 MainWindow.xaml 解析后  生成的窗体   作为程序启动时的主窗体



此外

该文件中的

![微信截图_20230716142828](WPF图片文件\微信截图_20230716142828.png)

**App.xaml.cs是对应的代码文件，用于编写应用程序的启动逻辑和事件处理程序。**



**2，MainWindow.xaml和MainWindow.xaml.cs：**
MainWindow.xaml是主窗口的布局文件，用于定义应用程序的主界面。MainWindow.xaml.cs是对应的代码文件，用于编写主**窗口的逻辑和事件处理程序**。

**3，其他.xaml和.xaml.cs文件：**
除了MainWindow.xaml外，还可以在项目中创建其他的.xaml文件用于**定义其他窗口、用户控件或页面**。相应的.xaml.cs文件包含对应的代码逻辑和事件处理程序。

4，Properties文件夹：
Properties文件夹**用于存放应用程序的一些配置文件**，如AssemblyInfo.cs，其中包含了应用程序的元数据和程序集相关的版本、作者信息等。

5，Resources文件夹：
Resources文件夹用于存放应用程序所需的各种资源文件，如图片、样式文件、字体等。这些**资源可以在XAML文件中进行引用和使用**。

6，References文件夹：
References文件夹用于存放项目引用的外部程序集文件，这些程序集通常是通过NuGet包管理器或手动添加到项目中的。

**7，App.config（可选）：**
App.config文件是应用程序的配置文件，存放一些应用程序的配置信息，如数据库连接字符串、日志配置等。

8，其他文件和文件夹：
根据项目的需求，可以在工程中添加其他的文件和文件夹，如资源文件夹、样式文件夹、脚本文件夹等。



### WPF自动生成的代码（后缀名为".g.i.cs"的文件代码）



这部分是  编译器第一次处理  XAML解析后，生成的CS类代码，此时还没有执行

其中 InitializeComponent（）   是编译器生成的组件初始化的函数代码，

接下来，才执行纯C#代码



在WPF（Windows Presentation Foundation）中，后缀名为".g.i.cs"的文件是自动生成的文件，它包含了XAML（eXtensible Application Markup Language）文件在编译期间所生成的代码。以下是对这种文件的详细解释和用途：

1. 自动生成代码：在WPF中，使用XAML可以定义用户界面的布局、样式和行为。当我们编译一个包含XAML的项目时，编译器会生成对应的代码文件，这些文件包含了XAML中定义的元素的实例化、事件处理和其他相关逻辑的代码。

2. 部分类：".g.i.cs"文件中生成的代码是部分类（partial class），它与XAML文件中定义的代码是相对应的。这样做的目的是为了将XAML中的声明与后续自动生成的代码分隔开，方便开发人员进行维护和扩展。

3. 提高性能：在编译运行时，WPF框架会**先**读取和解析XAML文件，创建相应的UI元素。通过将XAML文件**编译为".g.i.cs"文件中的CS代码**，可以避免每次运行应用程序时都重新解析XAML文件，提高了应用程序的性能。

4. 支持组件连接：由于".g.i.cs"文件中的代码是自动生成的，它可以实现将XAML文件中声明的UI元素与后台代码中的变量、属性或事件进行连接。在XAML中，可以使用"x:Name"属性给UI元素命名，在".g.i.cs"文件中可以通过这个命名来访问和操作对应的UI元素。

总之，后缀名为".g.i.cs"的文件是WPF中自动生成的代码文件，用于将XAML文件中的声明转换为可执行的代码，以实现界面的初始化、事件处理和与后台逻辑的连接等功能。













### 工程注意事项

我将WPF的窗口移动到一个文件夹下之后，它的设计器不显示了，为什么？？



当你将 WPF 窗口移到一个新的文件夹下时，WPF 的设计器可能无法正常显示的原因可能有以下几个：

1. 文件路径引用问题：WPF 窗口中使用的资源（如样式、控件模板等）可能会使用相对路径来引用其他文件或资源。当你将窗口移到新的文件夹下时，原来的相对路径可能会发生变化，导致资源引用失败。这可能会导致设计器无法正常显示。

解决方法：检查窗口中使用的资源引用路径，并确保它们相对于窗口文件的新位置是正确的。你可以使用相对路径或绝对路径来确保资源引用的正确性。

2. 命名空间冲突：如果你在窗口代码文件中使用了明确的命名空间设置，移动窗口到新的文件夹可能会导致命名空间与其他文件冲突，从而影响设计器的显示。

解决方法：检查窗口代码文件中的命名空间设置，确保唯一性。如果必要，更新相关引用的命名空间。

3. 其他文件依赖关系：WPF 窗口可能有其他文件依赖关系，如自定义控件、转换器等。当你移动窗口到新的文件夹下时，这些文件的引用路径可能会发生变化，从而导致设计器无法正确加载和显示这些文件。

解决方法：检查窗口所依赖的其他文件，更新它们的引用路径，确保它们与窗口文件的新位置相匹配。

4. Visual Studio 缓存问题：有时，Visual Studio 缓存可能会导致设计器无法正确显示。当你移动窗口到新的文件夹下时，尝试清理 Visual Studio 缓存，并重新打开解决方案以使设计器重新加载窗口。

解决方法：关闭 Visual Studio，删除解决方案文件夹下的 `.vs` 文件夹，并重新打开解决方案以重新加载窗口。

如果问题仍然存在，可以尝试在 Visual Studio 中创建一个新的空白窗口，查看设计器是否能够正常显示。如果新窗口可以正常显示，那么问题可能在于原窗口文件或所在文件夹的设置或配置中。









### 工程中xaml 文件中命名空间的说明

在WPF工程中，XAML文件中的命名空间（namespace）用于引用和使用各种类和控件。使用命名空间可以告诉编译器在哪里查找对应的类、属性和事件。

以下是对WPF工程中XAML文件中命名空间的使用的详细说明：

1. 引入默认命名空间：（只有一个）
   在XAML文件的根元素中，可以使用 `xmlns` 属性引入默认的命名空间，以 `xmlns="..."` 的形式指定。这样可以在XAML文件中直接使用命名空间中的类和属性，无需使用限定名。

   示例：

   ```xaml
   <Window x:Class="MyApp.MainWindow"
           xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
           xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
           Title="My Window" Width="800" Height="600">
       <!-- 在这里可以直接使用默认命名空间中的类和属性 -->
   </Window>
   ```

2. 引入其他命名空间：
   如果在XAML文件中需要使用其他命名空间中的类和属性，需要使用 `xmlns` 属性引入。可以使用 `xmlns:别名="命名空间"` 的形式指定命名空间和一个别名（prefix）。

   示例：

   ```xaml
   <Window x:Class="MyApp.MainWindow"
           xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
           xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
           xmlns:local="clr-namespace:MyApp.MyNamespace"
           Title="My Window" Width="800" Height="600">
       <!-- 在这里可以使用默认命名空间中的类和属性 -->
       <local:MyCustomControl />
   </Window>
   ```

   这里使用了 `xmlns:local="clr-namespace:MyApp.MyNamespace"` 将 `MyApp.MyNamespace` 命名空间引入，并指定了别名 `local`。然后可以使用 `local` 对应的别名来使用 `MyApp.MyNamespace` 命名空间中的类或属性。

   如果要引入的命名空间  位于外部程序集中，**可以使用 `xmlns:别名="clr-namespace:命名空间;assembly=程序集"` 的形式指定。**

   
   
3. 使用命名空间中的类和属性：
   引入命名空间后，可以在XAML文件中使用该命名空间中的类和属性。可以使用类的全名或者别名来引用类。在元素属性上，可以使用命名空间前缀或者默认命名空间的前缀（如果已经指定了默认命名空间）。

   示例：

   ```xaml
   <Window x:Class="MyApp.MainWindow"
           xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
           xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
           xmlns:local="clr-namespace:MyApp.MyNamespace"
           Title="My Window" Width="800" Height="600">
       <Grid>
           <local:MyCustomControl />
           <Button Content="Click" Grid.Column="1" />
       </Grid>
   </Window>
   ```

   这个示例中，使用了 `local:MyCustomControl` 来引入了自定义的控件 `MyCustomControl`，并在网格布局中添加了该控件。另外，`Button`元素中使用了默认命名空间中的属性 `Grid.Column`。

通过以上的步骤，你可以在WPF工程中的XAML文件中引入和使用所需的命名空间，以使用命名空间中的类、属性和事件。这使得你可以使用自定义的控件或者访问其他命名空间的功能，从而扩展和定制你的WPF应用程序。



x:Class   的作用是XAML解析器将包含它的一整条标签 （如 x:Class="MyApp.MainWindow"） 解析成C#类后，这个类的类名是什么

![微信截图_20230716140217](WPF图片文件\微信截图_20230716140217.png)

![](WPF图片文件\微信截图_20230716141503.png)









### XAML中顶级元素说明

在WPF中，顶级元素是指XAML文件中的根元素，它是整个XAML布局的最顶层元素。以下是WPF中常见的顶级元素：

1. Window（窗口）：Window是WPF中最常见的顶级元素，用于创建一个应用程序的主窗口。它包含了一个可视化的用户界面，可以包含其他的控件和元素。

2. Page（页面）：Page是用于创建应用程序中的页面的顶级元素。它类似于Window，但通常用于创建多个页面的导航应用程序。

3. UserControl（用户控件）：UserControl是一种自定义的可重用控件，可以作为顶级元素在XAML中定义。它通常用于将一组相关的控件和元素封装为一个单独的可重用组件。

4. Application（应用程序）：Application是WPF应用程序的顶级元素，它定义了应用程序的入口点和全局设置。**通常，一个WPF应用程序只有一个Application元素。** 

除了以上列举的顶级元素，还可以使用其他特定的顶级元素来实现特定的功能，比如WindowChrome（自定义窗口样式）、ResourceDictionary（资源字典）等。根据具体的需求和场景，选择合适的顶级元素来构建WPF应用程序的界面和功能。









### Grid面板的使用

当使用WPF中的`<Grid>`面板时，你可以通过行（Row）和列（Column）的定义来创建灵活的布局。`<Grid>`面板允许将子元素按行和列进行组织和布局，可以自由定位和调整子元素的大小和位置，此外允许嵌套。以下是一个详细示例，演示了如何使用`<Grid>`面板创建一个简单的布局：

```xaml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto" /> <!-- 第一行，高度根据内容自动调整 -->
        <RowDefinition Height="*" />    <!-- 第二行，剩余空间自动分配 -->
        <RowDefinition Height="100" />  <!-- 第三行，固定高度为100 -->
    </Grid.RowDefinitions>
    
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="200" /> <!-- 第一列，固定宽度为200 -->
        <ColumnDefinition Width="*" />   <!-- 第二列，剩余空间自动分配 -->
    </Grid.ColumnDefinitions>
    
    <!-- 子元素 -->
    <TextBlock Text="Hello, World!" Grid.Row="0" Grid.Column="0" />
    <Button Content="Click Me" Grid.Row="1" Grid.Column="1" />
    <Rectangle Grid.Row="2" Grid.ColumnSpan="2" Fill="LightGray" />
</Grid>
```

在这个示例中，我们定义了一个`<Grid>`容器，并在其内部使用`<Grid.RowDefinitions>`和`<Grid.ColumnDefinitions>`元素来定义行和列的布局。然后，在`<Grid>`内添加了三个子元素，这些子元素将根据定义的行和列进行布局。

- `<TextBlock>` 元素位于第一行第一列（`Grid.Row="0"`，`Grid.Column="0"`），文本内容为"Hello, World!"。
- `<Button>` 元素位于第二行第二列（`Grid.Row="1"`，`Grid.Column="1"`），显示为"Click Me"。
- `<Rectangle>` 元素位于第三行，跨越了两列（`Grid.Row="2"`，`Grid.ColumnSpan="2"`），并填充灰色背景。

通过设置行和列的`Height`和`Width`属性，我们可以定义不同行和列的大小和行为。

在示例中，你可以看到第一行根据文本内容自动调整高度，第二行根据剩余空间自动分配，第三行固定高度为100。对于列，第一列固定宽度为200，第二列根据剩余空间自动分配。

`Grid.Row`和`Grid.Column`属性用于指定子元素在`<Grid>`中的行和列的位置。`Grid.ColumnSpan`属性用于设置子元素跨越几列。

通过使用`<Grid>`面板，我们可以轻松创建和调整复杂的布局，将子元素放置在不同的网格单元中，并根据需求设置行和列的大小和行为。这提供了很大的灵活性，可以帮助我们构建各种界面和布局。



当然，我可以给你提供一个更详细的使用示例来说明如何使用`<Grid>`面板进行布局。以下示例展示了一个常见的登录界面布局：

```xaml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto" />
        <RowDefinition Height="Auto" />
        <RowDefinition Height="*" />
        <RowDefinition Height="Auto" />
        <RowDefinition Height="Auto" />
    </Grid.RowDefinitions>

    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="Auto" />
        <ColumnDefinition Width="*" />
    </Grid.ColumnDefinitions>

    <TextBlock Text="Login" FontSize="24" FontWeight="Bold"
               Grid.Row="0" Grid.ColumnSpan="2" 
               HorizontalAlignment="Center" VerticalAlignment="Center" />

    <TextBlock Text="Username:" Grid.Row="1" Grid.Column="0"
               VerticalAlignment="Center" Margin="10" />
    <TextBox Grid.Row="1" Grid.Column="1" Margin="10" />

    <TextBlock Text="Password:" Grid.Row="2" Grid.Column="0"
               VerticalAlignment="Center" Margin="10" />
    <PasswordBox Grid.Row="2" Grid.Column="1" Margin="10" />

    <StackPanel Grid.Row="3" Grid.ColumnSpan="2"
                Orientation="Horizontal" HorizontalAlignment="Center" Margin="10">
        <Button Content="Login" Margin="10" />
        <Button Content="Cancel" Margin="10" />
    </StackPanel>

    <TextBlock Text="Forgot password?" Grid.Row="4" Grid.ColumnSpan="2"
               HorizontalAlignment="Center" Margin="10" />
</Grid>
```

在这个示例中，我们使用`<Grid>`面板来创建一个简单的登录界面布局。以下是每个元素的功能：

- `<TextBlock>` 元素用于显示"Login"标题，它跨越了两列 (`Grid.ColumnSpan="2"`)，位于第一行。
- `<TextBlock>` 和 `<TextBox>` 元素组合用于输入用户名，位于第二行。
- `<TextBlock>` 和 `<PasswordBox>` 元素组合用于输入密码，位于第三行。
- `<StackPanel>` 元素用于放置登录和取消按钮，水平排列，位于第四行。
- `<TextBlock>` 用于显示"Forgot password?"，位于第五行。

通过设置行和列的`Height`和`Width`，我们可以控制每个元素的大小和布局。在这个示例中，我们使用了不同的行高 (`Height`) 来设置标题、输入框、按钮和其他文本的高度。

通过指定`Grid.Row`和`Grid.Column`属性，我们可以将每个元素放置在合适的行和列中。

使用`<Grid>`面板布局，我们可以轻松地创建灵活且易于维护的界面。通过调整行和列的大小和属性，并放置子元素在不同的位置，我们可以创建各种复杂的布局来满足不同的需求。

注意 ：：

如果是

```xaml
 <RowDefinition Height="30*" />
```

此处表示30所占比，比如说一共加起来有120，此处的30就表示30在120 中的占比高度（所占比例计算尺寸）



### StackPanel面板的使用

![微信截图_20230720095511](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\微信截图_20230720095511.png)

在C#中，StackPanel是一种布局面板，用于在WPF应用程序中管理和排列子元素。StackPanel将其子元素按照水平或垂直方向依次排列，直到达到面板的边界。以下是对StackPanel的使用进行详解：

1. 声明和实例化StackPanel：

   在XAML中，可以使用以下方式声明和实例化一个StackPanel：
   
   ```xml
   <StackPanel Name="myStackPanel">
       <!-- 子元素 -->
   </StackPanel>
   ```
   
   在后台代码中，可以使用以下方式实例化一个StackPanel：
   
   ```csharp
   StackPanel myStackPanel = new StackPanel();
   ```

2. 添加子元素：

   添加子元素可以通过XAML或者后台代码来完成。
   
   - 在XAML中，可以在StackPanel标签内部添加其他控件作为子元素：
   
     ```xml
     <StackPanel>
         <Button Content="Button 1" />
         <Button Content="Button 2" />
         <!-- 其他子元素 -->
     </StackPanel>
     ```
   
   - 在后台代码中，可以使用Children属性添加子元素：
   
     ```csharp
     Button button1 = new Button() { Content = "Button 1" };
     Button button2 = new Button() { Content = "Button 2" };
     
     myStackPanel.Children.Add(button1);
     myStackPanel.Children.Add(button2);
     ```

3. 设置布局方向：

   StackPanel提供了Orientation属性来设置子元素的排列方向，默认是垂直方向（Vertical）。
   
   - 在XAML中，可以通过设置Orientation属性来指定布局方向：
   
     ```xml
     <StackPanel Orientation="Horizontal">
         <!-- 子元素 -->
     </StackPanel>
     ```
   
   - 在后台代码中，可以通过设置Orientation属性来指定布局方向：
   
     ```csharp
     myStackPanel.Orientation = Orientation.Horizontal;
     ```

4. 其他属性和方法：

   StackPanel还提供了许多其他属性和方法，用于设置子元素的对齐方式、间距以及动态添加或删除子元素等操作。一些常用的属性和方法包括：
   
   - VerticalAlignment和HorizontalAlignment：设置子元素的垂直和水平对齐方式。
   - Margin：设置StackPanel与其父容器之间的空白边距。
   - Spacing：设置子元素之间的间距。
   - Children.Count：获取StackPanel中子元素的数量。
   - Children.Remove：移除指定的子元素。
   - Children.Insert：在指定位置插入子元素。
   
   通过使用这些属性和方法，可以更灵活地控制和管理StackPanel中的子元素。

总结来说，StackPanel是一种常用的布局面板，用于在WPF应用程序中按照水平或垂直方向排列子元素。通过设置Orientation属性、添加子元素以及调整其他属性，可以实现灵活的界面布局。



### Canvas面板的使用

![微信截图_20230720111813](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\微信截图_20230720111813.png)

在C#中，Canvas是一种布局面板，用于在WPF应用程序中实现自由定位的元素布局。Canvas允许你通过指定元素的位置（左上角坐标）来控制它们在界面上的位置。以下是对Canvas面板的使用进行详解：

1. 声明和实例化Canvas：

   在XAML中，可以使用以下方式声明和实例化一个Canvas：
   
   ```xml
   <Canvas Name="myCanvas">
       <!-- 子元素 -->
   </Canvas>
   ```
   
   在后台代码中，可以使用以下方式实例化一个Canvas：
   
   ```csharp
   Canvas myCanvas = new Canvas();
   ```

2. 添加子元素并进行定位：

   在Canvas中，子元素的位置可以通过设置Canvas的附加属性来进行定位，主要是Canvas.Left和Canvas.Top属性。
   
   - 在XAML中，可以使用Canvas.Left和Canvas.Top属性来指定子元素的位置：
   
     ```xml
     <Canvas>
         <Button Content="Button 1" Canvas.Left="50" Canvas.Top="50" />
         <Button Content="Button 2" Canvas.Left="150" Canvas.Top="100" />
         <!-- 其他子元素 -->
     </Canvas>
     ```
   
   - 在后台代码中，可以使用SetLeft和SetTop方法来指定子元素的位置：
   
     ```csharp
     Button button1 = new Button() { Content = "Button 1" };
     Button button2 = new Button() { Content = "Button 2" };
     
     Canvas.SetLeft(button1, 50);
     Canvas.SetTop(button1, 50);
     
     Canvas.SetLeft(button2, 150);
     Canvas.SetTop(button2, 100);
     
     myCanvas.Children.Add(button1);
     myCanvas.Children.Add(button2);
     ```

3. 其他属性和方法：

   Canvas还提供了其他一些属性和方法，用于设置元素的宽度、高度、层叠顺序等。
   
   - Width和Height：设置Canvas的宽度和高度。
   - Background：设置Canvas的背景颜色。
   - ZIndex：设置子元素的层叠顺序，数值越大表示越靠前。
   
   通过使用这些属性和方法，可以实现更灵活的元素布局和交互。

总结来说，Canvas是一种用于自由定位元素的布局面板，在WPF应用程序中可以使用Canvas来精确控制元素在界面上的位置。通过使用Canvas的附加属性或者相关方法，可以设置子元素的位置，实现像素级的定位。Canvas还提供了其他属性和方法，用于设置宽度、高度、层叠顺序等。通过合理使用Canvas，可以实现自由度较高的界面布局和元素定位。



### DockPanel 停靠面板的使用

![微信截图_20230720112120](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\微信截图_20230720112120.png)

在C#中，DockPanel是一种布局面板，用于在WPF应用程序中实现停靠位置的元素布局。DockPanel通过将子元素停靠在指定的边界位置来实现布局。以下是对DockPanel的使用进行详解：

1. 声明和实例化DockPanel：

   在XAML中，可以使用以下方式声明和实例化一个DockPanel：
   
   ```xml
   <DockPanel Name="myDockPanel">
       <!-- 子元素 -->
   </DockPanel>
   ```
   
   在后台代码中，可以使用以下方式实例化一个DockPanel：
   
   ```csharp
   DockPanel myDockPanel = new DockPanel();
   ```

2. 添加子元素并进行停靠：

   在DockPanel中，子元素可以通过设置DockPanel.Dock附加属性来指定停靠位置。可以将子元素停靠在四个边界位置：Top（上方）、Bottom（下方）、Left（左侧）和Right（右侧）。

   - 在XAML中，可以使用DockPanel.Dock属性来指定子元素的停靠位置：
   
     ```xml
     <DockPanel>
         <Button Content="Button 1" DockPanel.Dock="Top" />
         <Button Content="Button 2" DockPanel.Dock="Bottom" />
         <Button Content="Button 3" DockPanel.Dock="Left" />
         <Button Content="Button 4" DockPanel.Dock="Right" />
         <!-- 其他子元素 -->
     </DockPanel>
     ```
   
   - 在后台代码中，可以使用SetDock方法来指定子元素的停靠位置：
   
     ```csharp
     Button button1 = new Button() { Content = "Button 1" };
     Button button2 = new Button() { Content = "Button 2" };
     Button button3 = new Button() { Content = "Button 3" };
     Button button4 = new Button() { Content = "Button 4" };
     
     DockPanel.SetDock(button1, Dock.Top);
     DockPanel.SetDock(button2, Dock.Bottom);
     DockPanel.SetDock(button3, Dock.Left);
     DockPanel.SetDock(button4, Dock.Right);
     
     myDockPanel.Children.Add(button1);
     myDockPanel.Children.Add(button2);
     myDockPanel.Children.Add(button3);
     myDockPanel.Children.Add(button4);
     ```

3. 其他属性和方法：

   DockPanel还提供了其他一些属性和方法，用于设置子元素的大小、对齐方式以及最小大小限制等。
   
   - LastChildFill：设置一个布尔值，指示是否将最后一个子元素自动填充可用空间。
   - HorizontalAlignment和VerticalAlignment：设置DockPanel中非停靠子元素的水平和垂直对齐方式。
   - Width和Height：设置DockPanel的宽度和高度。

   通过使用这些属性和方法，可以实现更灵活的元素布局和交互。

总结来说，DockPanel是一种在WPF应用程序中实现停靠位置元素布局的布局面板。通过设置停靠属性，可以将子元素停靠在指定的边界位置，如上方、下方、左侧、右侧。DockPanel还提供了其他属性和方法，用于设置子元素的大小、对齐方式以及最小大小限制等。通过合理使用DockPanel，可以实现具有停靠功能的界面布局。





### wrapPanel 面板的使用

![微信截图_20230720112127](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\微信截图_20230720112127.png)

在C#中，WrapPanel是一种布局面板，用于在WPF应用程序中实现自动换行的元素布局。当子元素的宽度超过WrapPanel宽度时，WrapPanel会自动将子元素放置在下一行开始的位置，实现换行布局。以下是对WrapPanel的使用进行详解：

1. 声明和实例化WrapPanel：

   在XAML中，可以使用以下方式声明和实例化一个WrapPanel：
   
   ```xml
   <WrapPanel Name="myWrapPanel">
       <!-- 子元素 -->
   </WrapPanel>
   ```
   
   在后台代码中，可以使用以下方式实例化一个WrapPanel：
   
   ```csharp
   WrapPanel myWrapPanel = new WrapPanel();
   ```

2. 添加子元素：

   添加子元素可以通过XAML或者后台代码来完成。
   
   - 在XAML中，可以在WrapPanel标签内部添加其他控件作为子元素：
   
     ```xml
     <WrapPanel>
         <Button Content="Button 1" />
         <Button Content="Button 2" />
         <!-- 其他子元素 -->
     </WrapPanel>
     ```
   
   - 在后台代码中，可以使用Children属性添加子元素：
   
     ```csharp
     Button button1 = new Button() { Content = "Button 1" };
     Button button2 = new Button() { Content = "Button 2" };
     
     myWrapPanel.Children.Add(button1);
     myWrapPanel.Children.Add(button2);
     ```

3. 其他属性和方法：

   WrapPanel还提供了其他属性和方法，用于设置子元素的间距、对齐方式等。
   
   - Orientation：设置子元素的排列方向，默认是水平方向（Horizontal）。
   - ItemWidth和ItemHeight：设置子元素的宽度和高度，用于限制子元素的大小。
   - HorizontalAlignment和VerticalAlignment：设置子元素的水平和垂直对齐方式。
   - Margin：设置WrapPanel与其父容器之间的空白边距。
   
   通过使用这些属性和方法，可以实现更灵活的元素布局和交互。

总结来说，WrapPanel是一种布局面板，用于在WPF应用程序中实现自动换行的元素布局。通过添加子元素并设置相关属性，可以实现子元素的自动换行排列。WrapPanel还提供了其他属性和方法，用于设置子元素的间距、对齐方式等。通过合理使用WrapPanel，可以实现自动换行的界面布局。



### 标记扩展

在WPF中，标记扩展（Markup Extension）是一种特殊的语法，可以在XAML中动态地创建对象、设置属性和执行其他扩展功能。标记扩展的语法使用大括号 `{}` 括起来，位于XAML属性值内部。下面是一些常用的标记扩展及其详解：

1. 静态资源扩展（StaticResource）：
   使用 `{StaticResource}` 可以引用先前定义好的静态资源。这样可以将可重复使用的资源（如样式、模板、颜色等）定义在外部并重复引用，提高代码的重用性和可维护性。

   示例：`<Button Background="{StaticResource MyButtonBackground}" />`

2. 动态资源扩展（DynamicResource）：
   使用 `{DynamicResource}` 可以引用动态资源，这些资源的值在运行时可以根据程序的上下文发生改变。这样可以在需要动态切换样式或主题的场景中，实现运行时样式的变化。

   示例：`<Button Background="{DynamicResource MyButtonBackground}" />`

3. 绑定扩展（Binding）：
   使用 `{Binding}` 可以创建属性绑定，将属性与数据源进行绑定。这样可以实现数据的双向绑定、数据转换和数据校验等功能。

   示例：`<TextBox Text="{Binding UserName}" />`

4. 资源扩展（x:Static）：
   使用 `{x:Static}` 可以引用静态的成员，如类的静态字段、属性或常量。这样可以将代码中的常量值提取到XAML中，并进行重复使用。

   示例：`<TextBox Text="{x:Static local:MyConstants.AppName}" />`

5. 符号扩展（x:Null）：
   使用 `{x:Null}` 可以将属性值设置为 null，用于清除默认值或取消属性的设置。

   示例：`<Button Content="{x:Null}" />`

这只是一小部分WPF中可用的标记扩展，它们提供了一种强大的方式来在XAML中实现动态、灵活和可重用的功能。你还可以自定义标记扩展以满足特定需求。详细的标记扩展语法和用法可以在MSDN文档等资源中找到。



注意：：

静态资源 只在初始化时访问一次，之后将不再访问这个资源

动态资源 会在程序运行期间  任然会访问的资源







### 项目工程逻辑

注意界面的嵌入，先在 工程中 添加一个**用户控件** ,在控件逻辑中加入用户控件的使用

用户控件  会生成一个窗口类，可在业务逻辑中 new 一个调用即可





### Binding的个人理解

Binding是数据源与目标之间的桥梁，一般来说  源头是逻辑层的对象及属性，目标是UI层的控件对象

使用Binding时，最重要的是设置  源和路径

UI上的元素关心的是哪个属性值的变化，或者说**哪个属性值是你想送达UI元素的**，那这个属性就是Binding的路径（Path）

如图

![企业微信截图_20230806164223](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\企业微信截图_20230806164223.png)

ElementName    指定控件的对象名



Binding是一种自动机制，他只有传递的功能，只是跑腿

思考一个问题，如何使一个属性有能力  通知 目标 ，告诉他 Binding 的值已经改变

让属性所在的类继承 一个   实现了一个   INotifyPropertyChanged 接口，利用灯泡可快捷生成

在此类中的  对应的Binding的Path 属性中的  set语句中激发一个事件

语法详情如下

```C#
public int Value3
        {
            get { return value3; }
            set { 
                value3 = value;
                //在赋值后，马上进行一个通知，通知到绑定的对象，去更新的
                //这里的参数是指 this本实例中的  Value3  属性
                // ?是指判断是否为空
                PropertyChanged?.Invoke(this, new PropertyChangedEventArgs("Value3"));
            }
        }
```





UI层加入VM层的命名空间，并且指定类名后，可以直接 Binding VM层中该类的属性

详情如下图

![微信截图_20230729154256](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\微信截图_20230729154256.png)

在指定命名空间和相应的类名后

在接下来的控件Binding中就可以通过绑定VM层的类中的属性 Model1（类对象）间接绑定属性 Model1中的属性

![微信截图_20230729154316](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\微信截图_20230729154316.png)

![微信截图_20230729154325](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\微信截图_20230729154325.png)

注意啊，这里的绑定只是形式上的绑定，只是建立一种约定

那么要真正达成实质上的协议，还必须指定这个UI的数据上下文，给出一个实例对象，这才是真正建立实质上的连接

就好像你谈恋爱不结婚，有个毛用

如图

![微信截图_20230729171830](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\微信截图_20230729171830.png)



这是VM层类的源代码

那VM层在干啥呢，这里是对M层Model1类中数据的的实例化

![微信截图_20230729154341](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\微信截图_20230729154341.png)

这是VM调用的数据层（M层）的源码

![微信截图_20230729154655](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\微信截图_20230729154655.png)

其中UI中的按键   Binding 的是VM中Model1 的命令属性

这个命令属性 的数据类型Command类，他是一个完全继承自接口的类（灯泡一键实现，你懂的，里面做了部分代码修改）

如下图

![微信截图_20230729160834](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\微信截图_20230729160834.png)

那么关于控件中事件的处理，当事件发生时，Command类在内部利用委托处理流程上的逻辑（invoke）

比如说这里，事件发生时，通知外部关联的函数，让他们去执行（这就是流程上的逻辑）

那么具体的运算呢，在外面 （VM层）去执行关联的函数



关于按键具体逻辑，梳理一下

当按键按下，事件发生，在Command类内部通知去执行外部关联的订阅者

订阅者执行后，V3的值发生改变，同时 在M数据层的数据类中，触发事件通知UI 他Binding的值 同步更新









### StringFormat

在WPF中，`StringFormat`是一个用于格式化数据绑定输出的属性。

当你使用数据绑定将数据显示在控件上时，可以使用`StringFormat`属性来指定数据的格式化方式。`StringFormat`属性接受一个字符串参数，通过这个字符串参数你可以定义输出的格式。

以下是一些常见的`StringFormat`示例：

```xml
<TextBlock Text="{Binding Price, StringFormat='Price: {0:C}'}" />
<TextBlock Text="{Binding Birthdate, StringFormat='yyyy-MM-dd'}" />
<TextBlock Text="{Binding Percentage, StringFormat='Percentage: {0:P}'}" />
```

在第一个示例中，通过`StringFormat`属性将`Price`属性的值进行格式化，使用`{0:C}`将其转换为货币形式。

第二个示例演示了如何使用`StringFormat`来格式化日期，将`Birthdate`属性的值格式化为`yyyy-MM-dd`的形式。

第三个示例将`Percentage`属性的值转换为百分比形式，格式化为`Percentage: {0:P}`。

通过使用`StringFormat`，你可以根据自己的需求对数据进行格式化，例如日期、货币、百分比等。通过在数据绑定中设置`StringFormat`属性，你可以控制数据在界面上的显示方式。

请注意，`StringFormat`只能应用于支持格式化的数据类型，如数字、日期等，并且支持的格式化字符串取决于数据类型。

希望以上解释对你有所帮助。如有任何进一步的问题，请随时提问。





### ConverterCulture

在WPF中，`ConverterCulture`是一个用于指定数据转换器（`Converter`）在执行数据转换时所使用的文化（`Culture`）信息的属性。

`ConverterCulture`属性是用于数据绑定中的`Binding`对象以及值转换器（`IValueConverter`）接口的`Convert`和`ConvertBack`方法。它用于指定要使用的文化信息，以便在值转换期间正确地格式化和解析数据。

通过设置`ConverterCulture`属性，你可以为数据转换器提供一个特定的文化，以确保在不同的地区或语言环境下正确处理数据的格式。

以下是一个示例的XAML代码，展示了`ConverterCulture`属性的使用：

```xml
<Window.Resources>
    <local:MyConverter x:Key="myConverter" />
</Window.Resources>

<TextBlock Text="{Binding Amount, Converter={StaticResource myConverter}, ConverterCulture=fr-FR}" />
```

在上述示例中，我们首先定义了一个名为`myConverter`的自定义转换器（`MyConverter`）。然后，我们将`Amount`属性与该转换器绑定，并通过`ConverterCulture`属性指定了`fr-FR`作为转换器的文化信息。

这样，当`MyConverter`转换器执行数据转换时，将使用法国（`fr-FR`）的文化信息来格式化和解析数据。

通过使用`ConverterCulture`，你可以确保在不同的文化环境中，数据在界面上正确地显示和转换。

需要注意的是，`ConverterCulture`属性接受一个标识特定文化的字符串作为输入，如`fr-FR`表示法国法语。如果你不设置`ConverterCulture`，那么将使用当前系统的默认文化。

希望以上解释对你有所帮助。如有任何进一步的问题，请随时提问。



### UI线程上执行UI操作

`Application.Current.Dispatcher.Invoke()` 是*一种在UI线程上执行操作的方法*。**在WPF中，UI元素只能由创建它们的线程访问和更新**。当需要从 非UI线程 访问或更新UI元素时，我们需要使用`Dispatcher.Invoke()`方法将操作推送到UI线程上执行。确保该操作在UI线程上执行，以避免线程间的冲突和异常。

通过调用`Application.Current.Dispatcher.Invoke(() => { /* UI 更新代码 */ });`，我们可以在UI线程上安全地更新UI元素。在这种情况下，我们使用匿名方法来编写UI更新的代码

总之，`Application.Current.Dispatcher.Invoke()`允许我们在非UI线程上执行UI操作，并确保这些操作在UI线程上执行，以确保线程安全性和正确的UI更新。





### 将字符串消息  与 ASCII编码的字节数组的转换

`byte[] data = System.Text.Encoding.ASCII.GetBytes(message);` 是将字符串消息 `message` 转换为ASCII编码的字节数组。

在这段代码中，**`System.Text.Encoding.ASCII.GetBytes()` 方法用于将字符串转换为字节数组。**

ASCII编码是一种使用7位表示（即128个字符 127+1）的字符编码方案，可以将每个字符映射到一个唯一的整数值（0-127范围内）。这些整数值可以表示为字节数组。

`GetBytes()` 方法将字符串转换为对应的ASCII编码的字节数组。**每个字符被解释为一个字节**，并存储在数组中。返回的字节数组可以用于网络通信或其他需要以字节形式传输数据的场景。

在上述代码中，`message` 是要发送给客户端的文本消息。通过调用 `System.Text.Encoding.ASCII.GetBytes(message)`，我们将该消息转换为ASCII编码的字节数组，以便通过Socket发送给客户端。





上述代码片段涉及接收来自客户端的消息。

1. `byte[] buffer = new byte[4096];` 创建一个名为 `buffer` 的字节数组，用于存储从客户端接收到的数据。这里创建的数组大小是 4096 字节，表示最大可接收的数据大小为 4096 字节。

2. `await clientSocket.ReceiveAsync(new ArraySegment<byte>(buffer), SocketFlags.None);` 使用 `clientSocket` 对象的 `ReceiveAsync()` 方法进行异步接收操作。`ReceiveAsync()` 方法会将从客户端接收的数据写入到 `buffer` 数组中。`ArraySegment<byte>(buffer)` 表示接收数据时要写入的缓冲区。`SocketFlags.None` 表示没有任何标志设置。

3. `int bytesRead = ...` 该行代码是等待并获取实际接收到的字节数。`ReceiveAsync()` 方法返回一个整数值，表示实际从客户端接收到的字节数。这个值会保存在 `bytesRead` 变量中。

4. `string receivedMessage = System.Text.Encoding.ASCII.GetString(buffer, 0, bytesRead);` 使用 **`System.Text.Encoding.ASCII.GetString()` 方法将接收到的字节数组转换为字符串**。`GetString()` 方法将指定的字节数组从指定的索引位置开始解码为字符串。在这里，我们使用了前面接收到的字节数 `bytesRead` 来确保只解码接收到的有效数据部分。最后，将解码后的字符串保存在 `receivedMessage` 变量中。

综上所述，这段代码用于从客户端接收数据并将其转换为字符串，以便在服务端进行处理或显示。





### RadioButton

WPF中的RadioButton是一种用户界面控件，用于提供多个互斥选项供用户选择。当用户选中一个RadioButton时，其他的RadioButton会自动取消选中状态。

在WPF中，可以通过以下步骤来创建和使用RadioButton：

1. 在XAML文件中，通过RadioButton标记创建一个RadioButton控件，可以设置其内容、名称、选中状态等属性。例如：

```xaml
<RadioButton Content="Option 1" IsChecked="True" />
<RadioButton Content="Option 2" />
<RadioButton Content="Option 3" />
```

2. 可以将RadioButton放置在一个容器控件中，例如StackPanel或Grid，以便更好地管理和布局。例如：

```xaml
<StackPanel>
    <RadioButton Content="Option 1" IsChecked="True" />
    <RadioButton Content="Option 2" />
    <RadioButton Content="Option 3" />
</StackPanel>
```

3. 可以使用RadioButton的Checked事件来处理用户选择的逻辑。例如，在页面的代码后台，可以添加类似以下的事件处理程序：

```csharp
private void RadioButton_Checked(object sender, RoutedEventArgs e)
{
    RadioButton radioButton = sender as RadioButton;
    if (radioButton.IsChecked == true)
    {
        string option = radioButton.Content.ToString();
        // 执行选中选项后的逻辑
    }
}
```

4. 可以使用RadioButton的Group属性创建多个RadioButton的分组，使它们之间互斥。只有同一组中的RadioButton之间才会互斥。例如：

```xaml
<StackPanel>
    <RadioButton Content="Option 1" GroupName="Options" IsChecked="True" />
    <RadioButton Content="Option 2" GroupName="Options" />
    <RadioButton Content="Option 3" GroupName="Options" />
</StackPanel>
```

这样，当用户选择一个选项时，其他属于同一组的选项将自动取消选择。

以上是WPF中使用RadioButton控件的基本过程，你可以根据实际需求进一步定制RadioButton的样式、交互逻辑等。





### Template（详情见代码）

在WPF中，Template（模板）是一种用于定义控件外观和结构的机制。通过使用模板，你可以完全自定义控件的外观，包括控件的布局、样式、绘制和交互等方面。

在WPF中，模板主要使用XAML语言来定义。以下是使用模板的步骤：

1. 创建控件的模板：
   - 在XAML文件中，添加一个控件（例如Button）。
   - 添加一个名为"ControlTemplate"的<Control.Template>标签，并在其中定义控件的外观和结构。

```xaml
<Button>
    <Button.Template>
        <ControlTemplate>
            <!-- 在这里定义控件的外观和结构 -->
        </ControlTemplate>
    </Button.Template>
</Button>
```

2. 定义模板的内容：
   - 在ControlTemplate标签中，你可以使用其他控件和布局容器来设计控件的外观和结构。
   - 可以使用VisualStateManager来定义不同状态下的控件表现方式。

```xaml
<Button>
    <Button.Template>
        <ControlTemplate>
            <Grid>
                <Ellipse x:Name="Ellipse" Width="100" Height="100" Fill="Red" />
                <TextBlock Text="Click Me" HorizontalAlignment="Center" VerticalAlignment="Center" />
            </Grid>

            <ControlTemplate.Triggers>
                <Trigger Property="IsMouseOver" Value="True">
                    <Setter TargetName="Ellipse" Property="Fill" Value="Blue"/>
                </Trigger>
                <Trigger Property="IsPressed" Value="True">
                    <Setter TargetName="Ellipse" Property="Fill" Value="Green"/>
                </Trigger>
            </ControlTemplate.Triggers>
        </ControlTemplate>
    </Button.Template>
</Button>
```

在上面的例子中，一个简单的Button控件被定义为一个椭圆（Ellipse）和一个文本块（TextBlock）的组合。当鼠标移过按钮时，椭圆的填充颜色变为蓝色；当按下按钮时，椭圆的填充颜色变为绿色。

3. 将模板应用到控件上：
   - 在需要使用自定义模板的控件上，使用"Style"属性来引用该模板。

```xaml
<Button Style="{StaticResource MyButtonTemplate}" />
```

以上代码中，"MyButtonTemplate"是在资源字典中定义的按钮模板。

通过使用模板，你可以非常灵活地定制控件的外观和行为，以满足特定的设计需求。同时，WPF也提供了许多内置的控件模板，你可以根据需要进行调整和修改。如果你想进一步学习和探索模板的使用，可以查阅WPF官方文档或其他相关教程。







### 资源字典

如果说想将你自己设计好的样式，让其他文件也可以用

那么，在工程项目中类似用户控件一样，添加一个 资源字典

如图

![企业微信截图_20230806165940](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\企业微信截图_20230806165940.png)



注意，要在初始的APP的XAML文件中添加  资源字典

如图

![企业微信截图_20230806170739](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\企业微信截图_20230806170739.png)

红箭拖处就是你资源字典的文件名





### 动画的基本概念

设置一个按键的最简单动画

![企业微信截图_20230806171906](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\企业微信截图_20230806171906.png)

 

其他效果可以去参考 类中说明









### 样式



![企业微信截图_20230808154236](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\企业微信截图_20230808154236.png)





### 触发器

![企业微信截图_20230808154531](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\企业微信截图_20230808154531.png)



### 控件模版



![企业微信截图_20230808171659](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\企业微信截图_20230808171659.png)









### 数据模版

[WPF基础之控件模板、数据模板_wpf 控件模板_痕迹灬的博客-CSDN博客](https://blog.csdn.net/yigu4011/article/details/131302066)



## Binding的顶级理解

### 指定上下文DataContext

每一个控件容器，如果你Binding了一个数据来源，那么你就必须指定数据上下文

指定在哪里？？

你可以在这个控件容器以及这个容器的所有上级处指定，它找不到就会去上级找，一直找到最上级哪里

指定的方式有以下几种

1，直接在窗口处申明（不建议，除非代码结构足够简单）

![企业微信截图_20230808180814](D:\黄浒烨\TY--MD文件\C#\WPF图片文件\企业微信截图_20230808180814.png)

一般来说都是在  这个控件或者这个控件的直接上级  指定上下文

特别注意：：你绑定如果什么都不写，或者写一个点  “.”  ，那么默认的上下文，它会自己找默认的DataContext





2，在代码处申明
