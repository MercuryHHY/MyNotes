## （个人理解）

首先Win Form 是一个基于windows VS的UI界面设计工具，类似于QT的UI界面设计，只是QT是可以跨平台的而他只能在.NET平台上运行

个人感觉比QT方便一些



## C#中的UI设计操作



### 连接简单说明

在设计界面，点击属性窗口，上面有5个图标，选择其中的事件，此处有一系列事件的选择，

在设计界面每次创建一个事件，会在Design.cs 文件中生成一个  控件的事件与处理方法的连接代码 +=

在业务逻辑中如果不再需要此事件与控件的连接，那么可以在事件处理函数中 -= 切断此连接 

注意，在设计界面，创建事件双击即可跳转到事件处理函数





### 快捷操作说明

#### 右键菜单的使用

ContextMenuStrip：：当用户右键关联控件时，显示快捷菜单

要明白，这个窗口关联的是哪个界面或者是哪个控件，那么才可以在相应的窗口设置ContextMenuStrip选项



#### 复制

按住Ctrl键不放，点击一个控件，拖动，可以复制但也**仅仅**复制一个控件以及关联的事件，复制出来的控件，它的事件处理会调用原控件的事件处理函数





### 窗体的使用和说明

在窗口中，有一些类和容器，比如说 Controls(管理控件的容器，像按钮之类的控件都继承于它的Control类)

Control类对象  **以及**  继承于它的子类对象，才可以加入Controls容器

这里用的是父类指针指向子类对象的多态思想

那么具体呢，例如下面对  本窗口中Controls容器的遍历，筛选操作

![微信截图_20230626145535](picture\微信截图_20230626145535.png)



#### 打开一个新的子窗口

在C#的UI设计中，在一个窗口的控件的事件发生以后，打开一个新的子窗口，该怎么做？

在C#的UI设计中，可以通过以下步骤在一个窗口的控件事件发生后打开一个新的子窗口：

1. 在主窗口中，找到触发事件的控件（例如按钮）并双击打开其事件处理程序。

2. 在事件处理程序中，创建一个新的子窗口对象，例如：

```csharp
ChildForm childForm = new ChildForm();
```

这里的`ChildForm`是你要打开的子窗口的类名，你可以根据自己的需求修改。

3. 可选：如果需要传递数据给子窗口，可以在创建子窗口对象后设置其属性或调用其方法，例如：

```csharp
childForm.SomeProperty = someValue;
childForm.SomeMethod(someParameter);
```

4. 使用以下代码打开子窗口：

```csharp
childForm.ShowDialog();
```

使用`ShowDialog()`方法可以将子窗口以模态方式打开，即主窗口将被阻塞，直到子窗口关闭。如果你希望子窗口以非模态方式打开，可以使用`Show()`方法。

5. 如果需要在子窗口关闭后获取子窗口返回的结果，可以在子窗口关闭后检查其`DialogResult`属性或自定义的属性，例如：

```csharp
if (childForm.DialogResult == DialogResult.OK)
{
    // 子窗口返回了OK结果，执行相应的操作
}
```

这些步骤可以帮助你在C#的UI设计中，在一个窗口的控件事件发生后打开一个新的子窗口。请根据自己的需求和具体情况进行适当的调整和扩展。



### 事件的使用和说明

对用户的行为封装好的类，与QT类似



### 控件的属性说明

1，Tag 是控件中保存信息的属性

​		对各个控件的事件集中处理中，可以通过一些属性的值来区分所需要的控件

2，text是控件的文本信息，或者说是控件的名字

3，FormBorderStyle    窗口的边框样式

4，size      设置窗体或者控件的尺寸

5，StartPosition   窗体的开始位置

6，icon    可以在文件中选择图标来设置

7，Back   背景设置，，注意，如果控件的颜色与窗口的背景颜色不一致，那么可设置控件的背景颜色来保持一		致哦

8，Dock   设置控件放置的位置，布局

9，panel   设置区域的容器

10，TextAlign  ，imageAlign，对于控件中文本和图像的位置设置

11，AutoSize   自动默认的Size，打开还是关闭，关闭后可以手动设置控件变大变小

12，  当Flatstyle为Flat时，        FlatAppearance用于设置控件边框大小和颜色

​			如果想要消除控件边框，那么只需将  边框大小设置为0，或者将边框大小与背景保持一致都可

13，	





### 工具箱的使用说明

TextBox  文本框

DataGridView     数据的列表显示

timer   一个控制时间的组件





### 工程开发经验

#### 图片资源的重新绘制

在UI设计构成中，有些的图片放置在界面中，不是简单的放置，而是通过声明的一个`Graphics`对象，用于绘制图像，重新调整图像之后再使用，见下列代码说明

```C#
 private List<Bitmap> res = new List<Bitmap>
        {
            Properties.Resources._2Pawn,
            Properties.Resources._2Bishop,
            Properties.Resources._2Knight,
            Properties.Resources._2Rook,
            Properties.Resources._2Queen,
            Properties.Resources._2King,
            Properties.Resources.Pawn,
            Properties.Resources.Bishop,
            Properties.Resources.Knight,
            Properties.Resources.Rook,
            Properties.Resources.Queen,
            Properties.Resources.King
        };

private void resize()
        {
            Graphics graphic;//这个对象可以简单理解为一个工具
            for (int i = 0; i < res.Count; i++)
            {
                Bitmap bmp = new Bitmap(70, 70);
                graphic = Graphics.FromImage(bmp);
                graphic.DrawImage(res[i], 0, 0, 70, 70);
                graphic.Dispose();
                res[i] = bmp;
            }
        }

```

上述代码是一个名为`resize()`的方法，它将一组图像调整为固定的大小（70x70像素）。以下是代码的解释：

1. 声明一个`Graphics`对象，用于绘制图像。

2. 使用`for`循环遍历`res`列表中的每个图像。

3. 创建一个新的`Bitmap`对象，大小为70x70像素。

4. 使用`Graphics.FromImage()`方法将`graphic`对象与新创建的`Bitmap`对象相关联。使用`Graphics.FromImage`方法从`bmp`中获取图形操作的实例，将该实例赋值给`graphic`变量。

5. 使用`graphic.DrawImage()`方法将原始图像调整为70x70像素，并绘制到新的`Bitmap`对象上。

6. 释放`graphic`对象占用的资源。

7. 将调整大小后的图像（新的`Bitmap`对象）存储回`res`列表中。

这段代码可以在需要调整图像大小的场景中使用。它通过创建一个新的`Bitmap`对象，并使用`Graphics`对象将原始图像绘制到新的`Bitmap`对象上，从而实现了图像大小的调整。请确保`res`列表中包含要调整大小的图像，并在调用`resize()`方法之前初始化该列表。
