







## 此间心外无物

对这个世界保持饥渴感



## 注意事项

我目前数据库中存在2个数据库的服务端，以及3个客户端

为了区分服务端，用端口号区分

3306  的服务端 ======》》》  是我自己在网上下载的自由版本（默认）

3307  的服务端 ======》》》  是公司老版本管制的安装版

一定注意，默认的3306，在代码中就算不指定端口也能正常连接上默认的3306

但是3307不是默认的，一定切记要在代码的数据库连接字符串中**指定 端口号**

至于客户端，随便怎么玩，只是公司用的SQL脚本只能在老的 （3307）中执行

其次，3.0框架中的数据库连接字符串是在 APP.Config的初始化配置中提取的，去改这里

特别注意，启动项目的  自动生成的 配置文件中可能存在之前编译的端口号，

注意软件更新的时候不要将这个文件一同拷贝，不然会报错  无法连接数据库



注意，如果3306连接不上，参考一下方法

[完美解决：MySQL8报错：Public Key Retrieval is not allowed-CSDN博客](https://blog.csdn.net/white0718/article/details/131790493)





### **此外**

```
今天，使用mysql workbench 给一张表添加了一列varchar类型的列。在插入中文数据时出现

这是编码问题，只要将表的类型修改为utf-8就ok了。


alter table 数据库名.表名 convert to character set utf8;
执行完这条语句之后就可以插入中文数据啦。


如果多张表存在这个问题可以直接修改数据库的编码类型
alter database 数据名 character set utf8;


如果想在创建数据库时就解决这个问题可以在建表时加
ENGINE=InnoDB DEFAULT CHARSET=utf8


例如：
create table new
```



 update alarm set name = '预留' where NAME='';









## Helper

### CommonTool



### LinkPLC

![IPLC说明](D:\黄浒烨\TY--MD文件\HmxMCU工程说明书\PIC\IPLC说明.png)

1，Hmx_PLCBase是抽象类  ，IPLCBase是接口   两者都是对  **具体PIC类的行为与特征的描述**,

2，中间4个是4种具体的PIC连接类，行为与特征与 抽象层的大致一致，只是具体的实现细节不同

​	（实现细节依赖于接口）

3，最后的 IPLC类是 直接供给上层的（比如**VM层**）调用使用的，依赖于接口而不是依赖于具体的实现，在它里面定义了一个接口

如图

![接口定义](D:\黄浒烨\TY--MD文件\HmxMCU工程说明书\PIC\接口定义.png)

**这个接口**在程序最开始执行的时候就已经   根据APP.Config的程序集中PLC的类型，**实例化**（上面4种具体的PIC连接类中的一种）

如图

<img src="D:\黄浒烨\TY--MD文件\HmxMCU工程说明书\PIC\初始化PLC.png" alt="初始化PLC" style="zoom:67%;" />

并且IPLC类中的具体实现也是依赖于接口

如图

<img src="D:\黄浒烨\TY--MD文件\HmxMCU工程说明书\PIC\依赖于接口函数.png" alt="依赖于接口函数" style="zoom:67%;" />







### AbstractModel

#### BaseModel

##### GetEnumDescruption函数

这段代码是一个静态方法 `GetEnumDescruption`，它接受一个枚举类型的参数 `enumValue`，并返回该枚举值的描述信息。

下面是对这段代码的逐行解释：

1. `var field = enumValue.GetType().GetField(enumValue.ToString());` 通过 `GetType()` 方法获取 `enumValue` 的运行时类型，然后使用 `GetField()` 方法获取枚举值的 `FieldInfo` 对象。

2. `var objs = field.GetCustomAttribute(typeof(DescriptionAttribute));` 使用 `GetCustomAttribute()` 方法获取 `FieldInfo` 对象上应用的 `DescriptionAttribute` 特性对象。

3. `var descrip = (DescriptionAttribute)objs;` 将获取到的 `DescriptionAttribute` 强制转换为 `DescriptionAttribute` 类型，将其赋值给 `descrip` 变量。

4. `return descrip.Description;` 返回 `descrip` 对象的 `Description` 属性值，即枚举值的描述信息。

在使用这个方法时，你需要为枚举值定义一个带有 `DescriptionAttribute` 的描述，例如：

```csharp
public enum MyEnum
{
    [Description("枚举值1的描述")]
    Value1,

    [Description("枚举值2的描述")]
    Value2
}
```

然后可以调用 `GetEnumDescruption` 方法来获取枚举值的描述信息：

```csharp
MyEnum enumValue = MyEnum.Value1;
string description = GetEnumDescruption(enumValue);
Console.WriteLine(description);  // 输出 "枚举值1的描述"
```

这段代码利用了反射机制来获取枚举值的描述信息，通过读取 `DescriptionAttribute` 特性并获取其 `Description` 属性值来实现。这样可以方便地为枚举值提供附加的描述信息，以便在需要时获取和使用。









GetTableName

这段代码是一个虚拟方法 `GetTableName()`，用于获取对象的表名。

下面是对这段代码的逐行解释：

1. `if (this.GetType().IsDefined(typeof(TableNameAttribute), true))` 判断当前对象所属的类型是否应用了 `TableNameAttribute` 特性。`typeof(TableNameAttribute)` 表示要检查的特性类型，`true` 表示是否检查继承链上的特性。

2. `(TableNameAttribute)this.GetType().GetCustomAttribute(typeof(TableNameAttribute))` 通过 `GetCustomAttribute()` 方法获取对象所属类型上应用的 `TableNameAttribute` 特性对象，并将其强制转换为 `TableNameAttribute` 类型，赋值给 `tableNameAttr` 变量。

3. `if (tableNameAttr.TableName == null || tableNameAttr.TableName.Trim().Length == 0)` 判断获取到的 `TableNameAttribute` 对象的表名是否为空或空格。

4. `return this.GetType().Name;` 如果对象所属类型未应用 `TableNameAttribute` 特性或特性的表名为空，则返回对象所属类型的名称作为表名。

5. `return tableNameAttr.TableName;` 如果对象类型应用了 `TableNameAttribute` 特性且特性的表名不为空，则返回特性的表名。

这段代码用于获取对象的表名，通过检查对象所属类型是否应用了 `TableNameAttribute` 特性并获取其值。如果应用了该特性且表名不为空，则返回特性的表名；否则返回对象所属类型的名称作为表名。

例如，我们可以定义一个 `TableNameAttribute` 特性并将其应用到某个类：

```csharp
[AttributeUsage(AttributeTargets.Class)]
public class TableNameAttribute : Attribute
{
    public string TableName { get; set; }

    public TableNameAttribute(string tableName)
    {
        TableName = tableName;
    }
}

[TableName("Customers")]
public class Customer
{
    // ...
}
```

然后调用 `GetTableName()` 方法来获取对象的表名：

```csharp
Customer customer = new Customer();
string tableName = customer.GetTableName();
Console.WriteLine(tableName);  // 输出 "Customers"
```

在上面的示例中，`Customer` 类应用了 `TableNameAttribute` 特性，并将其表名设置为 "Customers"。使用 `GetTableName()` 方法可以获取到对象的表名为 "Customers"。如果类未应用 `TableNameAttribute` 特性，则返回类的名称作为表名。





#### BaseProxy

这段代码是一个基础代理类(BaseProxy)，它继承自RealProxy类，用于实现动态代理功能。

在构造函数中，传入被代理对象的类型(type)和实例(obj)，保存在成员变量instance中。

GetProxyInstance()方法返回代理对象的实例。

Invoke(IMessage msg)方法是动态代理的核心方法，当代理对象的方法被调用时，会首先进入该方法进行拦截和处理。通过获取调用的方法信息，包括被调用的方法(MethodBase)、参数等。然后通过调用AspectMethod()方法实现切面逻辑，AspectParam是传递给切面方法的参数。接着执行被代理对象的方法，并返回执行结果。

在AspectMethod()方法中，首先检查AspectParam参数是否为空，如果为空，则抛出异常。然后使用BaseFileTool.RecordLogToFile()方法记录日志。

总的来说，这段代码实现了一个基础的动态代理功能，通过继承RealProxy类并重写Invoke方法，在方法调用前后可以执行切面逻辑。



下面是一个简单的测试代码示例，用于演示如何使用BaseProxy类：

```csharp
public class MyService
{
    public void DoSomething()
    {
        Console.WriteLine("Doing something...");
    }
}

public class AspectProxy : BaseProxy
{
    public AspectProxy(Type type, object obj) : base(type, obj) { }

    public override void AspectMethod()
    {
        Console.WriteLine("Before method execution");
        base.AspectMethod();
        Console.WriteLine("After method execution");
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        MyService service = new MyService();
        AspectProxy proxy = new AspectProxy(typeof(MyService), service);

        // 获取代理对象
        MyService proxyInstance = (MyService)proxy.GetProxyInstance();

        // 通过代理对象调用方法
        proxyInstance.DoSomething();
    }
}
```

在上面的代码中，我们定义了一个MyService类，它有一个DoSomething()方法用于执行某些操作。然后定义了一个AspectProxy类，它继承自BaseProxy类，并重写了AspectMethod()方法，在方法执行前后输出日志。

在Main方法中，首先创建了一个MyService的实例service。然后创建了一个AspectProxy的实例proxy，将MyService的类型和实例传递给它。接着通过调用proxy的GetProxyInstance()方法获取代理对象的实例proxyInstance。

最后，通过proxyInstance调用DoSomething()方法，实际上会触发AspectProxy中的Invoke()方法，在执行前后会输出日志信息。

当我们运行上述测试代码时，将会输出以下结果：

```
Before method execution
[System.Runtime.Remoting.Messaging.MethodReturnMessageWrapper]
After method execution
```

这说明AspectProxy中的切面逻辑在方法执行前后都被成功执行了，并输出了相应的日志信息。







## 要点记录

### Timer

在C#中，Timer（计时器）是一个用于执行定时操作的类。它可以让你在指定的时间间隔内定期触发一个方法或事件。

要使用Timer，首先需要在代码中引入System.Timers命名空间。然后，可以通过以下步骤使用Timer：

1. 创建一个Timer对象，并指定触发间隔（以毫秒为单位）：
   ```
   Timer timer = new Timer(1000);
   ```

2. 添加一个事件处理程序或指定一个委托，用来处理定时触发的事件。可以使用匿名方法、lambda表达式或普通的命名方法：
   ```
   timer.Elapsed += (sender, e) => {
       // 在这里编写处理代码
   };
   ```

   或者

   ```
   timer.Elapsed += TimerElapsedEventHandler; // TimerElapsedEventHandler为自定义的方法
   ```

3. 启动Timer：
   ```
   timer.Start();
   ```

这样，Timer将在指定的时间间隔内触发事件或调用指定的委托。你也可以使用Stop方法停止Timer的触发。

需要注意的是，Timer是在一个线程池线程上运行的，**默认情况下是后台线程，因此程序不会等待Timer的执行完成**。

此外，还有其他类型的Timer，如System.Threading.Timer和System.Windows.Forms.Timer，它们有些许不同的用法和特点。



在使用C#中的Timer时，有一些注意事项需要注意：

1. 线程安全性：Timer是在一个线程池线程上运行的，因此在处理定时事件时，要确保任何访问共享数据的操作是线程安全的。可以使用锁或其他线程同步机制来保护共享数据。

2. 长时间操作：Timer的触发方法应该避免执行耗时的操作，因为它会阻塞Timer所在的线程，影响定时触发的准确性和整体性能。如果需要执行耗时操作，应考虑使用异步方法或另起线程来执行。

3. 定时器间隔：在设置定时器的触发间隔时，需要根据具体需求选择合适的时间间隔。如果间隔太长，可能会导致响应不及时；如果间隔太短，可能会对系统性能产生负面影响。需要根据实际情况进行调整。

4. 定时器的生命周期管理：在使用Timer时，要注意及时释放资源，避免内存泄漏。如果不再需要Timer，应使用Timer的Dispose方法进行释放或使用using语句来确保释放。

5. 跨线程操作：如果需要在定时触发的事件中更新UI或进行主线程相关的操作，需要使用合适的机制来确保在UI线程上执行，如使用Control.Invoke或Dispatcher.Invoke方法。

6. 异常处理：定时触发的事件可能会引发异常，为了保证程序的稳定性，应当对异常进行适当的处理，确保异常不会导致程序崩溃或无法预料的错误行为。

这些注意事项能够帮助你正确并安全地使用C#中的Timer。



### Stopwatch 

Stopwatch 是 C# 中的一个类，**用于测量运行时间的工具**。它提供了高精度的计时功能，可以用于分析代码的性能和优化。

要使用 Stopwatch，你需要进行以下步骤：

1. 首先，在代码文件的头部导入 `System.Diagnostics` 命名空间，以便使用 Stopwatch 类。
    ```csharp
    using System.Diagnostics;
    ```

2. 然后，创建 Stopwatch 对象并启动计时器。
    ```csharp
    Stopwatch stopwatch = new Stopwatch();
    stopwatch.Start();
    ```

3. 在需要计时的代码块执行完成后，停止计时器。
    ```csharp
    stopwatch.Stop();
    ```

4. 可以通过 Stopwatch 对象的 `Elapsed` 属性获取经过的时间，并以不同的格式进行显示或处理。
    ```csharp
    TimeSpan elapsed = stopwatch.Elapsed;
    Console.WriteLine($"Elapsed time: {elapsed}"); // 示例输出: Elapsed time: 00:00:01.2345678
    ```

通过以上步骤，你就可以用 Stopwatch 类来测量代码块的执行时间。请注意，Stopwatch 使用的是操作系统的高精度计时器，所以它提供了非常准确的计时结果。



在C#中，Stopwatch 类提供了两个属性用于获取经过的时间:

1. `ElapsedMilliseconds` 属性返回经过的时间（以毫秒为单位）作为整数。这个属性返回的是纯粹的毫秒数，不包含毫秒以下的细节。例如，如果经过时间是2.5秒，那么 `ElapsedMilliseconds` 属性将返回2500。

2. `Elapsed` 属性返回经过的时间作为一个 TimeSpan 对象。TimeSpan 是用于表示一段时间的结构体，它包含了小时、分钟、秒、毫秒等时间单位。你可以通过 `Elapsed` 属性获得一个 TimeSpan 对象，然后根据需要访问其属性来获取所需的时间信息。

   - 例如，通过 `Elapsed.TotalMilliseconds` 可以获取总共经过的毫秒数，包含毫秒以下的精确细节。

   - 通过 `Elapsed.TotalSeconds` 可以获取总共经过的秒数，包含秒以下的精确细节。

通常情况下，如果只需要获取经过的毫秒数或者只关心总共经过的时间，可以使用 `ElapsedMilliseconds`；如果需要更详细的时间信息，可以使用 `Elapsed` 属性。







### 一些LINQ查询的方法

```C#
this.productCount.Laser1Ear_Index = 
	this.Items.Where<Production>(p => p.Name == "激光1极耳序号").Select<Production, string>
	(p => p.Value)?.FirstOrDefault();
```

这段代码的作用是从 `Items` 集合中筛选出特定条件的对象，并提取其中的某个属性值赋给 `this.productCount.Laser1Ear_Index`。

具体逐步解释如下：

1. `this.Items` 是一个集合，假设它存储的是 `Production` 类型的对象。

2. `Where<Production>(p => p.Name == "激光1极耳序号")` 使用 LINQ 的 `Where` 方法对集合进行筛选，以满足 `Name` 属性等于 "激光1极耳序号" 的条件为准。这样即可筛选出符合条件的 `Production` 对象。

3. `Select<Production, string>(p => p.Value)` 使用 LINQ 的 `Select` 方法，对筛选结果中的每个 `Production` 对象，提取其 `Value` 属性的值，返回一个由这些值组成的字符串集合。

4. `?.FirstOrDefault()` 由 C# 的 ?. 和 FirstOrDefault() 方法组合而成。它表示在取得筛选结果的第一个元素之前，先判断集合是否为空。如果集合为空，则返回默认值，否则返回筛选结果集中的第一个对象。

5. 最后，将得到的结果赋值给 `this.productCount.Laser1Ear_Index` 属性。

简而言之，这行代码的目的是筛选 `Items` 集合中具有特定条件的对象，并提取对应的属性值作为结果，然后将结果赋值给 `productCount.Laser1Ear_Index` 属性。



### IGrouping<TKey, TElement>

要得到 `IGrouping<TKey, TElement>` 对象，通常需要进行分组操作并使用相应的 LINQ 查询或方法链。

下面我将以一个示例来说明如何得到并使用 `IGrouping<TKey, TElement>`：

假设有一个 `Production` 类，包含 `Name` 和 `Category` 属性。现在有一个 `List<Production>`，我们想按照 `Category` 进行分组，得到一组 `IGrouping<string, Production>` 对象。

```csharp
class Production
{
    public string Name { get; set; }
    public string Category { get; set; }
}

// 示例数据
List<Production> productions = new List<Production>
{
    new Production { Name = "Product 1", Category = "Category A" },
    new Production { Name = "Product 2", Category = "Category B" },
    new Production { Name = "Product 3", Category = "Category A" },
    new Production { Name = "Product 4", Category = "Category B" },
};

// 进行分组操作
var groupedData = productions.GroupBy(p => p.Category);

// 遍历每个分组
foreach (var group in groupedData)
{
    string category = group.Key; // 获取分组的键值

    Console.WriteLine($"Category: {category}");
    Console.WriteLine("Products:");

    foreach (var production in group)
    {
        Console.WriteLine(production.Name);
    }

    Console.WriteLine();
}
```

上述代码首先定义了一个 `List<Production>` 的示例数据，然后使用 `GroupBy()` 方法对该列表进行分组操作，按照 `Category` 属性进行分组。得到的结果是一组 `IGrouping<string, Production>` 对象。

之后，使用 `foreach` 遍历每个分组，通过 `Key` 属性获取分组的键值，并遍历分组内的每个 `Production` 元素。

你可以根据具体的需求对 `group` 进行排序、筛选、投影等操作，以及嵌套其他 LINQ 查询。

以上就是得到和使用 `IGrouping<TKey, TElement>` 的一个示例。你可以根据具体的场景和需求，灵活运用 `GroupBy()` 方法和相关的 LINQ 操作，来得到和处理分组数据。



`IGrouping<TKey, TElement>` 接口是 LINQ（Language Integrated Query）中用于分组操作的一部分。它表示一个具有相同键值的元素集合。

在具体应用中，你可以使用 `IGrouping<TKey, TElement>` 接口进行各种操作，例如：

1. 访问键值（Key）：通过 `Key` 属性可以获取当前分组的键值。
   ```csharp
   string key = group.Key;
   ```

2. 获取分组内的元素：使用 `foreach` 遍历 `IGrouping<TKey, TElement>` 对象，可获取该分组中的所有元素。
   ```csharp
   foreach (Production production in group)
   {
       // 对每个元素进行操作
   }
   ```

3. 使用 LINQ 操作进行筛选和投影：`IGrouping<TKey, TElement>` 可以和 LINQ 查询一起使用，进行筛选、投影和排序等操作。
   ```csharp
   var filteredGroup = group.Where(p => p.Quantity > 0); // 筛选数量大于0的元素
   
   var projectedGroup = group.Select(p => p.Name); // 投影出元素的名称
   
   var sortedGroup = group.OrderBy(p => p.Price); // 按价格对元素进行排序
   ```

4. 同时使用多个分组：通过嵌套的 LINQ 查询，可以同时使用多个分组进行复杂的数据分析。
   ```csharp
   var groupedData = data.GroupBy(p => p.Category).GroupBy(p => p.Year);
   
   foreach (var yearGroup in groupedData)
   {
       foreach (var categoryGroup in yearGroup)
       {
           // 在多个分组中进行操作
       }
   }
   ```

总之，`IGrouping<TKey, TElement>` 接口提供了一种方便的方式将元素按照键值进行分组，并且可以实现各种分组后的操作。通过结合 LINQ，你可以更灵活地处理和分析数据。



在实际使用中，你可以通过 LINQ 查询语法或方法链来操作 `IGrouping<TKey, TElement>`。下面我将分别介绍两种使用方式。

方式一：使用 LINQ 查询语法

你可以使用 LINQ 查询语法来对 `IGrouping<TKey, TElement>` 进行操作。下面是一些常见的用法示例：

1. 访问键值（Key）：
   ```csharp
   var groupedData = // 进行分组操作
   
   foreach (var group in groupedData)
   {
       string key = group.Key;
       // 对每个分组进行操作
   }
   ```

2. 获取分组内的元素：
   ```csharp
   var groupedData = // 进行分组操作
   
   foreach (var group in groupedData)
   {
       foreach (var element in group)
       {
           // 对每个元素进行操作
       }
   }
   ```

3. 使用 LINQ 操作：
   ```csharp
   var groupedData = // 进行分组操作
   
   var filteredGroup = from group in groupedData
                       where group.Sum(e => e.Quantity) > 0
                       select group;
   
   var projectedGroup = from group in groupedData
                        select new
                        {
                            Key = group.Key,
                            TotalPrice = group.Sum(e => e.Price)
                        };
   ```

方式二：使用方法链

你也可以使用方法链来操作 `IGrouping<TKey, TElement>`。下面是一些常见的用法示例：

1. 访问键值（Key）：
   ```csharp
   var groupedData = // 进行分组操作
   
   foreach (var group in groupedData)
   {
       string key = group.Key;
       // 对每个分组进行操作
   }
   ```

2. 获取分组内的元素：
   ```csharp
   var groupedData = // 进行分组操作
   
   foreach (var group in groupedData)
   {
       foreach (var element in group)
       {
           // 对每个元素进行操作
       }
   }
   ```

3. 使用 LINQ 操作：
   ```csharp
   var groupedData = // 进行分组操作
   
   var filteredGroup = groupedData.Where(group => group.Sum(e => e.Quantity) > 0);
   
   var projectedGroup = groupedData.Select(group => new
                       {
                           Key = group.Key,
                           TotalPrice = group.Sum(e => e.Price)
                       });
   ```

这些示例只是展示了 `IGrouping<TKey, TElement>` 的一些常见用法。实际上，你可以根据具体的需求进行更复杂的操作，包括筛选、投影、排序等。通过灵活运用 LINQ，你可以轻松地对分组数据进行处理和分析。



### ObservableCollection

在WPF和其他基于 .NET 的框架中，`ObservableCollection`是一种实现了`INotifyCollectionChanged`接口的集合类型。它提供了一种方便的方式来在集合发生变化时通知绑定到该集合的界面元素进行更新。

`ObservableCollection`允许你动态添加、删除和修改集合中的项，并确保这些更改会自动反映在绑定的界面上。

以下是一个简单示例，展示了如何使用`ObservableCollection`：

```csharp
using System.Collections.ObjectModel;

// 创建一个ObservableCollection实例
ObservableCollection<string> myCollection = new ObservableCollection<string>();

// 添加项到集合中
myCollection.Add("Item 1");
myCollection.Add("Item 2");
myCollection.Add("Item 3");

// 从集合中移除项
myCollection.Remove("Item 2");

// 使用索引修改集合中的项
myCollection[0] = "Updated Item 1";
```

在上述示例中，当我们向`ObservableCollection`中添加、删除或修改项时，它会自动引发`CollectionChanged`事件，这使得与该集合绑定的界面元素能够收到通知，并更新以反映这些更改。

在WPF中，你可以在XAML代码中使用`ObservableCollection`作为数据源。例如，你可以绑定一个`ItemsControl`控件的`ItemsSource`属性到`ObservableCollection`，以实现数据的动态显示。

希望这样能回答你的问题！如果还有其他问题，请随时提问。













## WPF

### 资源字典中的模版

控件模版

在HMXMCU的资源字典中

一个控件模版的使用说明

```XAML
<Style TargetType="Button">
        <Setter Property="Margin" Value="0,2" />
        <Setter Property="Padding" Value="10,5" />
        <!--<Setter Property="FontWeight" Value="ExtraBold"/>-->
        <Setter Property="Cursor" Value="Hand" />
        <Setter Property="Background" Value="#E1E1E1" />
        <Setter Property="BorderBrush" Value="#ADADAD" />
        <Setter Property="BorderThickness" Value="2" />
        <!--<Setter Property="ToolTip" Value="{Binding RelativeSource={x:Static RelativeSource.Self},Path=Content}"/>-->

        <Setter Property="Foreground" Value="Black" />
        <Setter Property="FrameworkElement.VerticalAlignment" Value="Center" />

        <Setter Property="HorizontalContentAlignment" Value="Center" />
        <Setter Property="VerticalContentAlignment" Value="Center" />

        <Setter Property="FontSize" Value="15" />

        <!--<Setter Property="Effect">
            <Setter.Value>
                <DropShadowEffect BlurRadius="20" Color="Gray" RenderingBias="Quality" ShadowDepth="5"/>
            </Setter.Value>
        </Setter>-->

    
    //这里是控件模版的定义
        <Setter Property="Template">
            <Setter.Value>
                <ControlTemplate TargetType="{x:Type Button}">
                    <Grid>
                        <Rectangle x:Name="rect"
                                   Fill="{TemplateBinding Background}"
                                   RadiusX="0"
                                   RadiusY="0"
                                   Stroke="{TemplateBinding BorderBrush}"
                                   StrokeThickness="{TemplateBinding BorderThickness}" />
                        <TextBlock Padding="{TemplateBinding Padding}"
                                   HorizontalAlignment="{TemplateBinding HorizontalContentAlignment}"
                                   VerticalAlignment="Center"
                                   FontSize="{TemplateBinding FontSize}"
                                   Foreground="{TemplateBinding Foreground}"
                                   TextTrimming="WordEllipsis"
                                   TextWrapping="Wrap">
                            <ContentPresenter />
                        </TextBlock>
                    </Grid>
                    <ControlTemplate.Triggers>
                        <Trigger Property="IsDefaulted" Value="True" />
                        <Trigger Property="IsMouseOver" Value="True">
                            <Setter Property="Foreground" Value="Black" />

                            <!--<Setter Property="RenderTransform">
                                <Setter.Value>
                                    <ScaleTransform CenterX="0.5" CenterY="0.5" ScaleX="1.05" ScaleY="1.05"/>
                                </Setter.Value>
                            </Setter>-->
                        </Trigger>
                        <Trigger Property="IsPressed" Value="True">
                            <Setter Property="IsEnabled" Value="True" />
                        </Trigger>
                    </ControlTemplate.Triggers>
                </ControlTemplate>
            </Setter.Value>
        </Setter>

        <Style.Triggers>
            <Trigger Property="IsFocused" Value="True">
                <Setter Property="Background" Value="LightGray" />
                <Setter Property="Foreground" Value="Green" />
                <Setter Property="BorderBrush" Value="#0292f9" />
                <Setter Property="BorderThickness" Value="2" />
                <Setter Property="Effect">
                    <Setter.Value>
                        <DropShadowEffect BlurRadius="20"
                                          RenderingBias="Quality"
                                          ShadowDepth="5"
                                          Color="LightBlue" />
                    </Setter.Value>
                </Setter>
            </Trigger>

            <!--<Trigger Property="IsEnabled" Value="False">
                <Setter Property="Background" Value="Black"/>
                <Setter Property="Foreground" Value="White"/>
                <Setter Property="Cursor" Value="Pen"/>
            </Trigger>-->
        </Style.Triggers>

    </Style>
```

在资源字典中设置一个控件样式，在样式中定义模版  Template

注意TemplateBinding 的意思是 外部申明这种控件是可以给出相应的参数值（依赖于外面）

控件模版的使用，要么是在资源里面自定义控件模版，然后在控件使用时用Template   动态/静态 引用你的模版

要么是在资源字典中指定控件样式时，一并指定模版如上所示





### Viewbox

在WPF（Windows Presentation Foundation）中，Viewbox是一个用于自动缩放和布局其内容的控件。它允许你将其子元素调整为父容器的大小，以便在不失真的情况下适应不同的窗口大小或布局需求。

使用Viewbox很简单。你只需将需要自动缩放的内容放置在Viewbox的内部，然后通过设置Viewbox的属性来控制缩放和布局的行为。以下是一个简单的示例：

```xaml
<Viewbox>
    <TextBlock Text="Hello, World!" FontSize="20" />
</Viewbox>
```

在上面的示例中，TextBlock的内容将自动缩放以适应Viewbox的大小。你可以根据需要调整Viewbox的属性，例如设置Stretch属性来指定内容的拉伸方式。默认情况下，Stretch属性设置为Uniform，即保持内容的宽高比并在父容器中居中显示。

这只是Viewbox的基本用法。根据你的具体需求，你还可以通过使用其他属性和嵌套来进一步定制和布局你的内容。









### AutoMonitor

#### 相关说明

在指定数据模版的控件样式时，按键绑定了一个命令，这个命令只用于 我自定义按键可编辑数据的按键（EnableEdit 按下触发）

那么 按键的  **IsEnabled**决定一个按键是否使能，是否能按下，是否能触发绑定的命令

ListView的资源绑定的是  ObservableCollection   （详情见上）





有一个必要的说明，数据模版如果绑定  “.”   那么会**将父节点的资源提取一次**

```XAML
<ListBox ItemsSource="{Binding autoMonitorModel.Parameter}" ScrollViewer.HorizontalScrollBarVisibility="Disabled" ScrollViewer.VerticalScrollBarVisibility="Disabled">
                <ListBox.ItemsPanel>
                    <ItemsPanelTemplate>
                        <!-- 注意这里的 UniformGrid 布局样式 就决定了 有多少空位  -->
                        <UniformGrid Columns="3" Rows="2" />
                        <!--<WrapPanel Orientation="Horizontal" />-->
                    </ItemsPanelTemplate>
                </ListBox.ItemsPanel>
                <ListBox.ItemTemplate>
                    <DataTemplate>
                        <GroupBox Width="{Binding ElementName=H1, Path=ActualWidth}"
                                  Height="{Binding ElementName=H1, Path=ActualHeight}"
                                  VerticalAlignment="Top"
                                  Header="{Binding Key}">
                            <Grid>
                                <!--  自适应高度  -->
                                <UniformGrid Rows="8">
                                    <Grid Name="T1" />
                                </UniformGrid>

                                <!--  表格数据  -->
                                <DataGrid 
                                    <DataGrid.Columns>
                                        <DataGridTemplateColumn Width="2*" Header="名称">
                                            <DataGridTemplateColumn.CellTemplate>
                                                <DataTemplate>
                                                    <!--  注意，这个Name绑定的是project里面的名称  -->
                                                    <TextBlock VerticalAlignment="Center"
                                                               FontSize="16"
                                                               Text="{Binding Name}"
                                                               ToolTip="{Binding RelativeSource={x:Static RelativeSource.Self}, Path=Text}" />
                                                </DataTemplate>
                                            </DataGridTemplateColumn.CellTemplate>
                                        </DataGridTemplateColumn>

                                        <DataGridTemplateColumn Width="1*" Header="值">
                                            <DataGridTemplateColumn.CellTemplate>
                                                <DataTemplate>
                                                    <Button 
                                                            Command="{Binding DataContext.ChangeValueCommand, RelativeSource={RelativeSource Mode=FindAncestor, AncestorType={x:Type ListBox}}}"
                                                            CommandParameter="{Binding Path=.}"
                                                            Content="{Binding Value}"                                                         
                                                            ToolTip="{Binding RelativeSource={x:Static RelativeSource.Self}, Path=Content}" />

                                                    <!--  数据模板 配置页面可用按钮与不可用按钮 注意这里的Attribute是表格里面的字段  -->
                                                    <DataTemplate.Triggers>                                                
                                                    </DataTemplate.Triggers>
                                                </DataTemplate>
                                            </DataGridTemplateColumn.CellTemplate>
                                        </DataGridTemplateColumn>
                                    </DataGrid.Columns>
                                </DataGrid>
                            </Grid>
                        </GroupBox>
                    </DataTemplate>
                </ListBox.ItemTemplate>
            </ListBox>

```













```XAML
<i:Interaction.Triggers>
        <i:EventTrigger EventName="Loaded">
            <i:InvokeCommandAction Command="{Binding LoadCommand}" CommandParameter="Loaded" />
        </i:EventTrigger>

        <i:EventTrigger EventName="Unloaded">
            <i:InvokeCommandAction Command="{Binding LoadCommand}" CommandParameter="Unloaded" />
        </i:EventTrigger>
    </i:Interaction.Triggers>
```

这段代码是使用了 WPF 的 `Interaction.Triggers` 和 `EventTrigger` 功能，用于在特定事件发生时执行绑定的命令。

以下是对代码的逐步解释：

1. `<i:Interaction.Triggers>` 标签是用来定义  交互触发器的起始标记。

2. `<i:EventTrigger EventName="Loaded">` 定义了一个事件触发器，当触发的事件为 "Loaded" 时执行后续逻辑。

3. `<i:InvokeCommandAction Command="{Binding LoadCommand}" CommandParameter="Loaded" />` 表示在事件触发时，执行与 `LoadCommand` 绑定的命令，并传递 "Loaded" 作为参数。

4. `</i:EventTrigger>` 结束了 "Loaded" 事件触发器的定义。

5. 同样的方式，`<i:EventTrigger EventName="Unloaded">` 定义了一个事件触发器，当触发的事件为 "Unloaded" 时执行后续逻辑。

6. `<i:InvokeCommandAction Command="{Binding LoadCommand}" CommandParameter="Unloaded" />` 表示在事件触发时，执行与 `LoadCommand` 绑定的命令，并传递 "Unloaded" 作为参数。

通过以上定义，当控件（如窗口、页面等）的 `Loaded` 事件被触发时，会执行与 `LoadCommand` 绑定的命令，并传递 "Loaded" 作为参数。同样地，当控件的 `Unloaded` 事件被触发时，会执行与 `LoadCommand` 绑定的命令，并传递 "Unloaded" 作为参数。

在具体的代码实现中，需要确保 `LoadCommand` 在 ViewModel 中正确地定义和实现，以便执行相应的逻辑。



在 WPF 中，`Loaded` 是一种事件触发器，它指示一个控件或一个窗口已经加载完毕并可见。

当控件（如窗口、页面、自定义控件等）被加载到可视化树中时，会引发 `Loaded` 事件。这表明控件已完成初始化并且在视觉上可见，可以进行进一步的操作。

一般情况下，你可以使用 `Loaded` 事件来执行一些初始化操作、加载数据、注册事件处理程序或执行其他与控件或窗口的生命周期相关的操作。

在 XAML 中，可以使用 `<EventTrigger EventName="Loaded">...</EventTrigger>` 的方式来创建 `Loaded` 事件的触发器，并在触发器的内容中编写需要执行的逻辑。

在代码中，你可以为控件添加一个 `Loaded` 事件处理程序，并在处理程序中编写你希望在控件加载时执行的逻辑。

总之，`Loaded` 事件触发器表示某个控件或窗口已完成加载并可见，可以用于在加载完成后执行相应的操作。







#### ToolTip

```xaml
<TextBlock Text="{Binding Name}" VerticalAlignment="Center" FontSize="16" ToolTip="{Binding RelativeSource={x:Static RelativeSource.Self}, Path=Text}" />
```

这段代码定义了一个 TextBlock 控件，并设置了一些属性和绑定关系。

详细解释如下：

- `Text="{Binding Name}"`：通过绑定 `Name` 属性，将 TextBlock 的文本内容设置为由数据上下文（ViewModel）中的 `Name` 属性提供的值。这意味着 TextBlock 将展示 `Name` 属性的值作为文本内容。

- `VerticalAlignment="Center"`：指定了 TextBlock 在垂直方向上的对齐方式为居中对齐。这将使 TextBlock 在其可用空间内相对居中显示。

- `FontSize="16"`：设置 TextBlock 的字体大小为 16 像素。这将影响 TextBlock 的文本显示的字体大小。

- `ToolTip="{Binding RelativeSource={x:Static RelativeSource.Self}, Path=Text}"`：设置了 TextBlock 的工具提示（ToolTip）内容。通过 Binding 的方式，在工具提示中展示 TextBlock 当前的文本内容。基于 `RelativeSource.Self` 的设置，表示将 TextBlock 本身作为绑定源，并通过 `Path=Text` 指定要获取的属性路径，即 TextBlock 的文本内容。

简而言之，这段代码创建了一个具有绑定关系、样式和工具提示功能的 TextBlock 控件，用于显示由数据上下文中的 Name 属性提供的文本内容，并在工具提示中显示 TextBlock 的文本内容。另外，将 TextBlock 在垂直方向上居中对齐，并设置字体大小为 16。







#### ObjectDataProvider

ObjectDataProvider 是一个在 WPF 中用于将对象作为数据源提供给绑定的特殊数据提供程序。

ObjectDataProvider 提供了一种简单的方式来使用对象和方法作为数据源，并将其与 XAML 中的控件进行绑定。它主要用于以下几种情况：

1. 当你需要将一个对象的属性或方法作为数据源来绑定到控件时，可以使用 ObjectDataProvider。

2. 当你需要调用一个静态方法来获取数据，并将其作为数据源与控件进行绑定时，可以使用 ObjectDataProvider。

使用 ObjectDataProvider 的步骤如下：

1. 创建 ObjectDataProvider 对象，并设置其属性。可以设置 ObjectType（类型）、MethodName（方法名）等。

2. 在 XAML 中使用 StaticResource 或者 Binding 的方式引用这个 ObjectDataProvider。

3. 绑定目标控件的 DataContext 属性或其他相关属性到 ObjectDataProvider，以便接收从数据源中提供的数据。

4. 使用绑定方式，将控件的属性与 ObjectDataProvider 的返回值绑定，以便获取并显示数据。

下面是一个简单的示例，展示了如何在 XAML 中使用 ObjectDataProvider：

```xml
<Window.Resources>
    <ObjectDataProvider x:Key="MyDataProvider" ObjectType="{x:Type local:MyClass}" MethodName="GetData" />
</Window.Resources>

<TextBlock Text="{Binding Source={StaticResource MyDataProvider}, Path=Result}" />
```

在这个示例中，我们创建了一个 ObjectDataProvider，并设置了 ObjectType 为 `MyClass`，MethodName 为 `GetData`。然后，我们通过绑定将 ObjectDataProvider 的 **Result** 属性绑定到 TextBlock 的 Text 属性上，**实现将 GetData 方法的返回值显示在 TextBlock 上**。

注意

`Result` 是一个属性，被用于在 `TextBlock` 的绑定中引用数据源对象的特定属性。在这段代码中，`Result` 是 `MyClass` 类中的一个属性。

在给定的代码片段中，我们只能看到 `ObjectDataProvider` 的定义。要了解 `Result` 属性的具体实现和定义，您需要查找或检查 `MyClass` 类的代码，特别是在 `GetData` 方法中。

`Result` 属性可能是 `MyClass` 类中的一个公共属性，用于保存 `GetData` 方法返回结果的值。您可以在 `MyClass` 类的代码中查找类似以下的属性定义：

```csharp
public string Result { get; set; }
```

这只是一个示例，实际的 `Result` 属性可能有不同的类型和实现。要找到 `Result` 属性的具体定义，请检查 `MyClass` 类的代码或相关文档。

需要注意的是，你需要根据具体的业务逻辑和数据源的类型，来设置 ObjectType 和 MethodName 的值，以便正确地获取数据并绑定到控件上。









```xaml
<ListBox.ItemsPanel>
                    <ItemsPanelTemplate>
                        <UniformGrid Columns="3" Rows="2" />
                        <!--<WrapPanel Orientation="Horizontal" />-->
                    </ItemsPanelTemplate>
                </ListBox.ItemsPanel>
```

这段代码定义了 ListBox 的 ItemsPanel，用于指定 ListBox 中项的布局方式。

解释如下：

```xml
<ListBox.ItemsPanel>
    <ItemsPanelTemplate>
        <UniformGrid Columns="3" Rows="2" />
        <!--<WrapPanel Orientation="Horizontal" />-->
    </ItemsPanelTemplate>
</ListBox.ItemsPanel>
```

在这段代码中，我们使用了 ItemsPanelTemplate 来定义 ListBox 的项的布局方式。

- `<UniformGrid Columns="3" Rows="2" />`：通过使用 UniformGrid 来定义项的布局。UniformGrid 是一个均匀分布项的布局面板，通过设置 Columns 和 Rows 可以指定每行和每列的项的数量。

- `<WrapPanel Orientation="Horizontal" />`：通过注释 `UniformGrid` 行并取消注释 WrapPanel，可以改为使用 WrapPanel 来定义项的布局。WrapPanel 是一个自动换行的面板，可以按水平或垂直方向自动换行显示项。

你可以根据具体需求选择 UniformGrid 或 WrapPanel，或者使用其他布局方式来定义 ListBox 的项的布局。这样可以根据你的设计要求，自定义项的位置和排列方式。





#### ScrollViewer

`ScrollViewer` 是一个用于显示可滚动内容的控件。它在界面中创建一个可滚动的视图区域，使用户能够在该区域内滚动内容，适用于需要展示大量内容或者超出显示区域的内容的情况。

在使用 `ScrollViewer` 控件时，通常需要将需要滚动的内容放置在 `ScrollViewer` 内部，通过设置 `Content` 属性来指定需要滚动的内容。

下面是一个使用 `ScrollViewer` 的简单示例：

```xml
<ScrollViewer>
    <!-- 需要滚动的内容 -->
</ScrollViewer>
```

你可以将需要滚动的内容放在 `ScrollViewer` 标签内，例如一个 `StackPanel`、一个 `Grid` 或者其他控件。当内容超出可视区域时，`ScrollViewer` 将显示垂直滚动条或水平滚动条（或两者皆有），用于滚动内容。

除了基本的滚动功能，`ScrollViewer` 还提供了许多其他属性和方法来自定义滚动体验，例如设置滚动条的可见性、滚动速度、翻页模式等。

需要注意的是，当在 `ScrollViewer` 中放置的内容过多时，可能会影响性能。因此，在设计界面时，应该合理使用 `ScrollViewer` 控件，避免在整个界面上滚动大块内容。





#### ItemsControl

[WPF基础之控件模板、数据模板_wpf 控件模板_痕迹灬的博客-CSDN博客](https://blog.csdn.net/yigu4011/article/details/131302066)

`ItemsControl` 是一个用于显示集合数据的控件。它可以将一个集合中的元素以指定的方式进行展示，例如在列表中显示、以网格排列等。`ItemsControl` 提供了一种方便的方式来呈现和布局多个相似的元素。

在使用 `ItemsControl` 控件时，需要完成以下几个步骤：

1. 定义数据源：首先，需要定义一个数据源，也就是用于存储要显示的数据集合。这可以是一个集合，如列表、数组或集合类，也可以是一个绑定到数据源的集合属性。

2. 设定 `ItemsSource`：将数据源绑定到 `ItemsControl` 的 `ItemsSource` 属性上。这样，`ItemsControl` 就知道要显示哪些数据。

3. 定义数据项模板：通过创建一个 `DataTemplate`，定义如何显示每个数据项的外观。模板可以包含控件和布局，用于呈现数据项中的属性或者自定义数据。

4. 设置 `ItemsControl` 的外观：根据需要设置 `ItemsControl` 控件的外观，包括容器的样式、布局方式、滚动条等。

下面是一个简单示例，在其中使用 `ItemsControl` 来显示一个字符串集合：

```xml
<ItemsControl ItemsSource="{Binding MyCollection}">
    <ItemsControl.ItemTemplate>
        <DataTemplate>
            <TextBlock Text="{Binding}" />
        </DataTemplate>
    </ItemsControl.ItemTemplate>
</ItemsControl>
```

在这个示例中，`ItemsSource` 属性绑定到一个名为 `MyCollection` 的集合属性。`ItemTemplate` 定义了以 `TextBlock` 显示每个数据项的方式。

通过这样的设置，`ItemsControl` 将自动将数据源中的每个元素作为数据项应用数据模板，并以相应的方式进行显示。这使得在界面中动态显示集合数据变得更加简单和灵活。



##### 补充说明



```XAML
 <ItemsControl.ItemsPanel>
                        <ItemsPanelTemplate>
    <WrapPanel />
                        </ItemsPanelTemplate>
                    </ItemsControl.ItemsPanel>
```

这代码意思是，在指定ItemsControl的ItemsPanel**布局容器**，又在里面指定布局容器的模版为 <WrapPanel />

`WrapPanel` 是一个面板控件，它会将子项按照水平方向排列，并在需要时自动换行到下一行。也就是说，这段代码指定了子项的布局方式为以水平方向排列，当空间不足时自动换行。

通过使用这段代码，可以将 `ItemsControl` 中的子项以瀑布流的方式进行布局，自动将子项在水平方向上进行排列，并在需要时进行换行显示。这种布局适合处理不定数量的项，并且能够利用空间更加高效地展示数据。



#### ItemTemplate 

在 WPF 中，ItemTemplate 是用于定义 ListBox、ListView、ComboBox 等控件中每个项的显示方式的一种机制。

ItemTemplate 是一个 DataTemplate 对象，它确定了如何呈现数据项的外观和布局。通过 ItemTemplate，你可以自定义每个项的外观，将数据以某种特定的方式呈现给用户。

使用 ItemTemplate 的步骤如下：

1. 定义一个 DataTemplate，并在其中指定你想要用来显示数据项的控件和布局。

```xml
<ListBox ItemsSource="{Binding MyItems}">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <!-- 用于呈现每个项的控件和布局 -->
        </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox>
```

2. 在 DataTemplate 内部，使用各种控件和布局来设计每个项的外观。可以使用绑定来显示数据项的属性。

```xml
<ListBox ItemsSource="{Binding MyItems}">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <StackPanel Orientation="Horizontal">
                <Image Source="{Binding Image}" Width="50" Height="50" />
                <TextBlock Text="{Binding Name}" Margin="10,0,0,0" />
            </StackPanel>
        </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox>
```

在这个示例中，我们使用了一个 StackPanel 控件来组织每个项的布局。每个项显示了一个图像（通过绑定 `Image` 属性）和一个名称（通过绑定 `Name` 属性）。你可以根据需要选择不同的布局控件和设置不同的属性来满足你的设计要求。

3. 在 DataTemplate 中，可以使用数据绑定来获取数据项的属性。通过在绑定路径中指定相应的属性，将数据与界面元素进行关联。

4. 如果有需要，你还可以为数据项定义 ItemContainerStyle，用于给每个项的外观应用样式或属性设置。

```xml
<ListBox ItemsSource="{Binding MyItems}">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <!-- 用于呈现每个项的控件和布局 -->
        </DataTemplate>
    </ListBox.ItemTemplate>
    <ListBox.ItemContainerStyle>
        <Style TargetType="ListBoxItem">
            <Setter Property="Foreground" Value="Blue" />
        </Style>
    </ListBox.ItemContainerStyle>
</ListBox>
```

在这个示例中，我们定义了一个样式，并将它应用于 ListBoxItem。样式设置了选中项文本的前景色为蓝色。

总而言之，ItemTemplate 是用于定义 ListBox、ListView、ComboBox 等控件中每个项的呈现方式的一种机制。通过使用 ItemTemplate，你可以自定义每个项的外观、布局和数据绑定，使其更符合你的需求。











### SafeMap



### EnableSwitch

#### 使用说明

用户控件中定义了一些样式

主控件布局中

grd1，grd2 是用于下面的  数据模版使用时，规定模版中数据与控件的自适应宽度

在指定数据模版的容器时，指定了容器的样式为  WrapPanel  布局

在指定数据模版的数据样式时，特别注意 使用了ObjectDataProvider中的类方法返回的类属性值，目的是为了区分不同用户是否具有使能的权限





#### Viewbox

在WPF（Windows Presentation Foundation）中，Viewbox是一种布局容器，用于自动缩放和调整其内容以适应可用空间。

Viewbox将其子元素按比例缩放，以填充Viewbox的可用空间，并保持内容的宽高比不变。通过使用Viewbox，你可以实现自适应布局，并确保内容在不同大小的窗口或容器中以一致的比例显示。

要在WPF中使用Viewbox，首先需要在XAML中将其作为父容器来包含所需的内容。例如：

```xaml
<Viewbox>
    <!-- 内容 -->
</Viewbox>
```

然后，将你希望进行自适应缩放的内容放置在Viewbox中。Viewbox将根据可用空间的大小自动调整内容的尺寸。

请注意，Viewbox的自适应缩放会导致内容的质量损失，特别是当内容包含文本或细节较多的图形时。因此，在使用Viewbox时，要确保内容以较高的分辨率或大小提供，以便在缩放时保持清晰度。





#### ScrollViewer

在WPF中，`ScrollViewer`是一个容器控件，它提供了滚动功能，用于展示具有大量内容的区域。`ScrollViewer`可以用于水平和/或垂直的滚动，让用户能够在可视区域内导航和查看内容。

以下是一个简单的示例，说明如何在WPF中使用`ScrollViewer`：

```xaml
<ScrollViewer>
    <!-- 在这里放置你的内容 -->
</ScrollViewer>
```

你可以在`ScrollViewer`中放置其他控件或者内容，包括文本、图像、面板等。当内容超出`ScrollViewer`的可视区域时，滚动条将自动出现，用户可以使用滚动条来滚动和查看内容。

你也可以通过设置`HorizontalScrollBarVisibility`和`VerticalScrollBarVisibility`属性来控制水平和垂直滚动条的可见性，例如：

```xaml
<ScrollViewer HorizontalScrollBarVisibility="Auto" VerticalScrollBarVisibility="Auto">
    <!-- 在这里放置你的内容 -->
</ScrollViewer>
```

此处，`Auto`属性值表示滚动条仅在需要时才可见，你也可以将其设置为`Visible`以始终显示滚动条。

希望以上信息对你有所帮助！如果有更多问题，请随时提问。







#### RelativeSource

`RelativeSource` 是在 WPF（Windows Presentation Foundation） 中用于**指定绑定上下文的一种方式**。它允许你引用其他元素或绑定的上层元素作为数据源，以便在绑定时获取相关数据。

`RelativeSource` 通常在 XAML 中的绑定表达式中使用。它的语法一般如下：

```
{Binding Path=SomeProperty, RelativeSource={RelativeSource Mode=ModeType, AncestorType=AncestorType}}
```

其中：

- `ModeType` 是一个枚举值，用来指定相对源的模式。常用的模式有：
  - `FindAncestor`：查找祖先元素。
  - `Self`：使用自身元素作为源。
  - `PreviousData`：在集合中查找上一个数据项。
- `AncestorType` 是一个类型引用，用于指定要查找的祖先元素的类型。

通过使用 `RelativeSource`，你可以在绑定表达式中引用其他元素，以获取这些元素的特定属性或数据，而不是仅仅依赖于当前元素的上下文。

以下是一个示例，展示如何使用 `RelativeSource` 将一个 `Button` 的背景颜色绑定到它外部 `Grid` 的前景颜色：

```xml
<Button Content="Click Me" Background="{Binding RelativeSource={RelativeSource Mode=FindAncestor, AncestorType={x:Type Grid}}, Path=Foreground}" />
```

在这个例子中，`Background` 属性通过 `RelativeSource` 设置为 `FindAncestor` 模式，查找类型为 `Grid` 的祖先元素。然后使用 `Path` 属性指定要绑定的属性为 `Foreground`，从而将 `Button` 的背景颜色与外部 `Grid` 的前景颜色进行绑定。



特别注意

```xaml
CommandParameter="{Binding .}"
```

意思是命令参数是当前数据源







### ParamSet



#### GroupName

在 WPF（Windows Presentation Foundation）中，GroupName是用于对一组相关的元素进行分组的属性。它通常用于 RadioButton 或 CheckBox 这样的控件，用于实现互斥选择的功能。

通过将一组 RadioButton 或 CheckBox 的 GroupName 属性设置为相同的值，这些元素将自动形成一个组。只有同一组中的元素中的一个可以被选中，其它元素将自动取消选择。

以下是一个示例，演示了如何在 XAML 中使用 GroupName 属性：

```xml
<StackPanel>
    <RadioButton GroupName="MyGroup">Option 1</RadioButton>
    <RadioButton GroupName="MyGroup">Option 2</RadioButton>
    <RadioButton GroupName="MyGroup">Option 3</RadioButton>
</StackPanel>
```

在这个示例中，三个 RadioButton 元素被分组，并且它们的 GroupName 属性值都设置为 "MyGroup"。这意味着用户只能选择其中一个选项，而不能同时选择多个选项。

希望这可以帮助你理解 WPF 中的 GroupName 属性的用法。如果你有任何进一步的问题，请随时提问。
