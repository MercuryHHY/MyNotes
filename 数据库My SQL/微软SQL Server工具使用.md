

## 创建和打开SQL Server

### 第一步

如图

<img src="数据库文档图片\微信截图_20230629143604.png" alt="微信截图_20230629143604" style="zoom:50%;" />

在此配置管理器的

![微信截图_20230629143824](数据库文档图片\微信截图_20230629143824.png)

打开SQL server 服务器

或者在计算机管理中找到此选项，一样的



### 第二步

打开SQL server图形工具studio  ，连接到服务器，如图

![微信截图_20230629144301](数据库文档图片\微信截图_20230629144301.png)



服务器名称：： 

​						服务器所在的  计算机名 或者  IP地址

​						英文符号  '.'  表示的是默认当前主机的 计算机名

​						当然，如果想访问外地的数据库服务器（其他电脑上的数据库服务器），请输入他							的IP地址

身份验证：：

​						Windows身份验证：：用当前主机Windows账号验证，可直接访问当前主机的数据									库服务器

​						SQL  Server 身份验证：：需要数据库服务器允许的（DCL创建并保存好的）用户									名和密码  



注意：：创建的数据库名称不可重名





## 数据库的备份迁移

### 第一步：分离A电脑上的数据库

右键创建的数据库名，选择任务，选择分离，点击成功后

生成一个文件，该文件位置同样的也在一开始创建数据库的文件位置，拷贝该文件到U盘即可

### 第二步：在B电脑上添加已有数据库

在对象资源管理器中，右键对象资源  数据库，选择附加，进入如下界面

![微信截图_20230629154318](C:\Users\gg\Desktop\TY--MD文件\数据库My SQL\数据库文档图片\微信截图_20230629154318.png)

点击添加

进入

![微信截图_20230629154433](C:\Users\gg\Desktop\TY--MD文件\数据库My SQL\数据库文档图片\微信截图_20230629154433.png)

选择所需的数据库数据文件，点击确定后，上一个界面的关联界面中会出现

相关的数据信息和日志文件，再次确定即可



特别注意：： 分离出来的数据库数据文件不可重命名，因为数据库数据文件保存的内部信息中 在分离时已经确定，分离后重命名会导致附加时出错



## 数据库的登录说明

首先用Windows身份登录，流程如下

![微信截图_20230630045200](数据库文档图片\微信截图_20230630045200.png)



注意事项：：

![微信截图_20230630045440](数据库文档图片\微信截图_20230630045440.png)





## 数据库的文件说明



![微信截图_20230630121259](数据库文档图片\微信截图_20230630121259.png)



### T-SQL与SQL的说明

T-SQL（Transact-SQL）是一种扩展的SQL（Structured Query Language）语言。SQL是一种用于管理和操作关系型数据库的标准查询语言，而T-SQL是由Microsoft开发的用于在Microsoft SQL Server数据库管理系统中执行查询和管理数据库的扩展版本。

如果您打算使用Microsoft SQL Server数据库，那么学习T-SQL是很重要的，因为它是与该数据库系统紧密相关的查询语言。T-SQL具有SQL的基本功能，并添加了一些特定于Microsoft SQL Server的功能和扩展，如存储过程、触发器、用户定义函数等。

如果您打算使用其他关系型数据库系统，例如Oracle、MySQL或PostgreSQL等，那么学习SQL是更为通用和广泛适用的选择。SQL是一种标准化的查询语言，几乎所有关系型数据库系统都支持它。

总而言之，如果您计划使用Microsoft SQL Server，那么学习T-SQL是必要的。如果您打算使用其他关系型数据库系统，那么学习SQL是更加通用和适用的选择。无论您学习哪种语言，了解SQL的基本概念和语法都是非常有帮助的。



### 用T-SQL语言生成一个创建一个数据库的代码，并且指定数据库大小

要在T-SQL中生成一个创建数据库并指定数据库大小的代码，您可以使用`CREATE DATABASE`语句的`SIZE`选项。以下是一个示例：

```sql
USE master;
GO

IF NOT EXISTS(SELECT name FROM sys.databases WHERE name = 'YourDatabaseName')
BEGIN
    CREATE DATABASE YourDatabaseName
    ON PRIMARY
    (
        NAME = 'YourDatabaseName_Data',
        FILENAME = 'C:\YourDatabaseName_Data.mdf',
        SIZE = 100MB,
        MAXSIZE = UNLIMITED,
        FILEGROWTH = 10MB
    )
    LOG ON
    (
        NAME = 'YourDatabaseName_Log',
        FILENAME = 'C:\YourDatabaseName_Log.ldf',
        SIZE = 50MB,
        MAXSIZE = 2GB,
        FILEGROWTH = 5MB
    );
    PRINT 'Database created successfully.';
END
ELSE
BEGIN
    PRINT 'Database already exists.';
END
```

将上述代码中的"YourDatabaseName"替换为您想要创建的数据库的名称。您还需要根据需要更改文件路径和文件名。在上述示例中，我们分别为数据文件和日志文件指定了初始大小、最大大小和文件增长量。

此代码通过`CREATE DATABASE`语句创建一个新的数据库，并使用`ON PRIMARY`和`LOG ON`子句分别指定主要数据文件和日志文件。在每个子句中，我们使用`NAME`选项指定文件的逻辑名称，`FILENAME`选项指定文件的物理路径和文件名，`SIZE`选项指定文件的初始大小，`MAXSIZE`选项指定文件的最大大小，`FILEGROWTH`选项指定文件的增长量。

请注意，在执行此代码之前，确保您具有足够的权限来创建数据库和指定文件路径。

特别注意：： 这里的GO  与SQL里的英文分号意思一致，表示这段操作语句结束



### 用T-SQL语言生成一个创建一个数据库的表代码

要使用T-SQL语言生成创建数据库表的代码，您可以使用`CREATE TABLE`语句。以下是一个示例：

```sql
USE YourDatabaseName;
GO

IF NOT EXISTS(SELECT * FROM sys.objects WHERE object_id = OBJECT_ID(N'dbo.YourTableName') AND type in (N'U'))
BEGIN
    CREATE TABLE dbo.YourTableName
    (
        ID INT PRIMARY KEY,
        Name NVARCHAR(50),
        Age INT,
        Email NVARCHAR(100)
    );
    PRINT 'Table created successfully.';
END
ELSE
BEGIN
    PRINT 'Table already exists.';
END
GO
```

将上述代码中的"YourDatabaseName"替换为您要创建表的数据库的名称。将"YourTableName"替换为您要创建的表的名称。在`CREATE TABLE`语句中，我们定义了表的结构，包括列名和数据类型。在上述示例中，我们创建了一个具有ID、Name、Age和Email列的表。

此代码通过`CREATE TABLE`语句创建一个新的表，并使用`IF NOT EXISTS`条件来检查表是否已存在。如果表不存在，则创建表并打印成功消息。如果表已经存在，则打印表已存在的消息。

在执行此代码之前，请确保您具有足够的权限来创建表和在指定的数据库中执行操作。



