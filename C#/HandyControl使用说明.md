





# HandyControl

文档参考

D:\黄浒烨\参考文档





## 开始

先加Netget包            HandyControl  3.4.0

注意要在APP.xaml中添加资源

```XAML 
<ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <!--  <ResourceDictionary Source="pack://application:"  -->
                <ResourceDictionary Source="pack://application:,,,/HandyControl;component/Themes/SkinDefault.xaml" />
                <ResourceDictionary Source="pack://application:,,,/HandyControl;component/Themes/Theme.xaml" />
            </ResourceDictionary.MergedDictionaries>
</ResourceDictionary>
```



使用示例

```xaml 
 <Label Width="60" Height="60" Style="{StaticResource LabelInfo}" />
```

添加资源或者用命名空间标识

如图

![1](D:\黄浒烨\TY--MD文件\C#\HandyControl_PIC\1.png)

hc 命名空间中有已经做好的控件模版和样式，直接用

注意要在页面上加命名空间

```XAML
xmlns:hc="https://handyorg.github.io/handycontrol"
```







## Label



![2](D:\黄浒烨\TY--MD文件\C#\HandyControl_PIC\2.png)



![3](D:\黄浒烨\TY--MD文件\C#\HandyControl_PIC\3.png)



- `BorderElement.CornerRadius="119"`：这个属性指定了边框的圆角半径大小，其中值为119。边框的圆角半径决定了边框角落的圆弧程度，越大则圆角越明显。
- `BorderBrush="{StaticResource SuccessBrush}"`：这个属性指定了边框的笔刷，也就是边框的颜色或绘画样式。`StaticResource SuccessBrush`是指从资源中获取名为"SuccessBrush"的笔刷进行边框的填充。
- `BorderThickness="1"`：这个属性指定了边框的宽度，其中值为1。边框的宽度决定了边框线条的粗细程度，越大则边框线条越粗。





## TextBox

```XAML
<TextBox Width="260"
                     Height="60"
                     HorizontalAlignment="Left"
                     VerticalAlignment="Top"
                     hc:InfoElement.Necessary="True"
                     hc:InfoElement.Placeholder="请设置数量！"
                     hc:InfoElement.Symbol="*"
                     hc:TitleElement.Title="编码："
                     hc:TitleElement.TitlePlacement="Top"
                     hc:TitleElement.TitleWidth="60"
                     Style="{StaticResource TextBoxExtend}"
                     Text="123"-
                     TextWrapping="Wrap" />
```

- `VerticalAlignment="Top"`：这个属性指定了文本框的垂直对齐方式，这里设置为靠上对齐。
- `hc:InfoElement.Necessary="True"`：这个属性指定了信息元素的必要性，设置为True表示该文本框是必填项。
- `hc:InfoElement.Placeholder="请设置数量！"`：这个属性指定了信息元素的占位文本，当文本框为空时显示的提示文字为"请设置数量！"。
- `hc:InfoElement.Symbol="*"`：这个属性指定了信息元素的符号，这里设置为星号(*)。
- `hc:TitleElement.Title="编码："`: 这个属性指定了标题元素的标题文本，设置为"编码："。
- `hc:TitleElement.TitlePlacement="Top"`：这个属性指定了标题元素的位置，这里设置为位于文本框顶部。
- `hc:TitleElement.TitleWidth="60"`：这个属性指定了标题元素的宽度，其中值为60像素。
- `Style="{StaticResource TextBoxExtend}"`：这个属性指定了文本框的样式，从资源中获取名为"TextBoxExtend"的样式应用于该文本框。
- `Text="123"`：这个属性指定了文本框的文本内容，设置为"123"。
- `TextWrapping="Wrap"`：这个属性指定了文本框的文本换行方式，设置为Wrap表示文本会自动换行。



## PasswordBox

```XAML
<PasswordBox Width="120"
                         VerticalAlignment="Center"
                         hc:InfoElement.Placeholder="请输入密码"
                         hc:TitleElement.Title="密码："
                         hc:TitleElement.TitlePlacement="Left"
                         PasswordChar="*"
                         Style="{DynamicResource PasswordBoxExtend}" />
```

- `hc:InfoElement.Placeholder="请输入密码"`：这个属性指定了信息元素的占位文本，当密码输入框为空时显示的提示文字为"请输入密码"。
- `hc:TitleElement.Title="密码："`: 这个属性指定了标题元素的标题文本，设置为"密码："。
- `hc:TitleElement.TitlePlacement="Left"`：这个属性指定了标题元素的位置，这里设置为位于密码输入框的左侧。
- `PasswordChar="*"`：这个属性指定了密码输入框显示的字符，设置为"*"表示输入的字符会被用星号(*)替代。
- `Style="{DynamicResource PasswordBoxExtend}"`：这个属性指定了密码输入框的样式，从动态资源中获取名为"PasswordBoxExtend"的样式应用于该密码输入框。



## Button

```XAML
<Button Width="129"
                    hc:IconElement.Geometry="{StaticResource AddGeometry}"
                    Background="{StaticResource SuccessBrush}"
                    Content="按键2"
                    Foreground="Black"
                    Style="{StaticResource ButtonPrimary}" />
```

- hc:IconElement.Geometry  设置图标
- 















