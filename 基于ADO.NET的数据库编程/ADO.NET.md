## 前言

C#工程怎么连接访问 SQLServer 中的数据库数据呢？？？？

利用 ADO.NET 技术

### ADO.NET 是什么？

ADO.NET（ActiveX Data Objects .NET）是.NET框架中用于访问和操作各种数据源的一组数据访问技术。它提供了一种可扩展的、高性能的数据访问层，用于连接到数据库、执行查询、更新数据以及处理数据。

以下是使用ADO.NET的一些重点：

1. 数据提供程序（Data Providers）：ADO.NET使用数据提供程序来连接到不同类型的数据源。每个数据提供程序都提供了一组类和方法，用于与特定类型的数据源进行交互。例如，`System.Data.SqlClient`是用于连接到SQL Server数据库的数据提供程序，`System.Data.OleDb`用于连接到OLE DB数据源，`System.Data.Odbc`用于连接到ODBC数据源等。

2. 连接对象（Connection）：`SqlConnection`是ADO.NET中用于与SQL Server数据库建立连接的类。您可以使用连接字符串指定数据库的位置和其他连接参数。使用连接对象，您可以打开和关闭数据库连接，并执行数据库操作。

3. 命令对象（Command）：`SqlCommand`是用于执行SQL语句或存储过程的类。您可以将SQL查询或存储过程名称与命令对象关联，并使用命令对象执行数据库操作，如查询数据、插入、更新和删除数据。

4. 数据读取器（DataReader）：`SqlDataReader`是一种只进只读的数据流，用于从数据库中检索数据。使用数据读取器，您可以逐行读取查询结果，并将数据存储在变量中进行处理。

5. 数据集对象（DataSet）：`DataSet`是内存中的数据容器，用于存储从数据库中检索的数据。数据集可以包含多个数据表，每个表都可以包含多个数据行和列。使用数据集，您可以在断开连接的情况下操作和处理数据。

6. 事务处理（Transaction）：ADO.NET提供了事务处理功能，用于在数据库操作中实现原子性、一致性、隔离性和持久性（ACID）的特性。您可以使用事务对象（`SqlTransaction`）来开始、提交或回滚事务。

7. 参数化查询（Parameterized Query）：为了防止SQL注入攻击和提高性能，ADO.NET支持参数化查询。您可以使用参数对象（`SqlParameter`）将参数值传递给查询，而不是将参数值直接嵌入到SQL语句中。

这些是使用ADO.NET的一些重点。通过使用这些类和技术，您可以连接到数据库，执行查询和更新操作，并处理和操作数据。请注意，使用ADO.NET时需要注意安全性和性能方面的最佳实践，例如避免拼接字符串来构建SQL查询，而是使用参数化查询来保护应用程序免受SQL注入攻击。





### 该怎么学呢

学习ADO.NET时，以下是一些重点和步骤：

1. 理解基本概念：开始学习ADO.NET之前，了解基本的数据库概念和术语是很重要的。熟悉数据库、表、列、行、SQL查询等基本概念将帮助您更好地理解ADO.NET的工作原理。

2. 熟悉.NET框架：ADO.NET是.NET框架的一部分，因此熟悉.NET框架的基本概念和语法是必要的。了解C#或VB.NET等.NET编程语言，并熟悉.NET中的类、对象、集合和基本语法将有助于您更好地理解和使用ADO.NET。

3. 学习数据提供程序：ADO.NET使用数据提供程序来连接到不同类型的数据源。学习和理解不同类型的数据提供程序，如`System.Data.SqlClient`、`System.Data.OleDb`和`System.Data.Odbc`，以及它们的特点和用法。

4. 连接到数据库：了解如何使用ADO.NET连接到数据库是重要的。学习连接字符串的格式和参数，以及如何创建和管理数据库连接对象。熟悉连接的生命周期，包括打开、关闭和释放连接。

5. 执行查询和更新操作：学习如何使用命令对象（`SqlCommand`）执行SQL查询和更新操作。了解如何构建SQL语句或调用存储过程，并将其与命令对象关联。学习如何执行查询、插入、更新和删除操作，并处理执行结果。

6. 数据读取和处理：学习如何使用数据读取器（`SqlDataReader`）从数据库中检索数据。了解如何逐行读取查询结果，并将数据存储在变量中进行处理。学习如何处理不同类型的数据，如整数、字符串、日期等。

7. 使用数据集：了解如何使用数据集（`DataSet`）来操作和处理数据。学习如何创建数据集、添加数据表、填充数据、更新数据以及处理数据表之间的关系。了解数据集的优点和用法，并学习如何在断开连接的情况下操作数据。

8. 事务处理：学习如何使用事务对象（`SqlTransaction`）来实现事务处理。了解如何开始、提交和回滚事务，以保证数据库操作的原子性、一致性、隔离性和持久性。

9. 参数化查询：学习如何使用参数对象（`SqlParameter`）来执行参数化查询。了解如何将参数值传递给查询，并避免直接将参数值嵌入到SQL语句中，以提高安全性和性能。

10. 错误处理和异常处理：学习如何处理和处理数据库操作中的错误和异常。了解如何捕获和处理异常，以及如何处理连接错误、查询错误和数据处理错误。

11. 最佳实践和性能优化：了解使用ADO.NET的最佳实践和性能优化技巧。学习如何提高数据库查询和更新操作的性能，如使用索引、优化查询语句、批量操作等。

以上是学习ADO.NET的一些重点和步骤。通过深入学习和实践这些概念和技术，您将能够更好地使用ADO.NET连接到数据库、执行查询和更新操作，并处理和操作数据。





## C#中数据库的具体使用

对于不同的DBMS 比如MySQL ，SQL Server  

![微信截图_20230701110851](ADO.NET  Picture\微信截图_20230701110851.png)

本质上，是利用已经继承封装好的类库代码（API）

所以注意：：：

要给出相应的命名空间 

```C#
//引入需要的命名空间
using System.Data.SqlClient;

```



### 生成使用C#连接并操作数据库的代码，并给出解释

以下是使用C#连接并操作数据库的示例代码：

```csharp
using System;
using System.Data.SqlClient;

namespace DatabaseConnectionExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 定义连接字符串
            string connectionString = "Data Source=ServerName;Initial Catalog=DatabaseName;User ID=UserName;Password=Password";

            // 创建数据库连接对象
            using (SqlConnection connection = new SqlConnection(connectionString))
            {
                try
                {
                    // 打开数据库连接
                    connection.Open();

                    // 执行查询操作
                    string query = "SELECT * FROM Customers";
                    //用`SqlCommand`类创建了一个查询对象，并将查询字符串和数据库连接对象传递给它
                    SqlCommand command = new SqlCommand(query, connection);
                    //使用`ExecuteReader()`方法执行查询，并使用`SqlDataReader`类读取查询结果。
                    SqlDataReader reader = command.ExecuteReader();

                    // 读取查询结果,在`while`循环中，我们逐行读取查询结果，并将数据打印到控制台。
                    while (reader.Read())
                    {
                        string customerId = reader["CustomerID"].ToString();
                        string companyName = reader["CompanyName"].ToString();
                        string contactName = reader["ContactName"].ToString();

                        Console.WriteLine($"Customer ID: {customerId}, Company Name: {companyName}, Contact Name: {contactName}");
                    }

                    // 关闭数据阅读器
                    reader.Close();

                    // 执行更新操作
                    string updateQuery = "UPDATE Customers SET CompanyName = 'New Company' WHERE CustomerID = 'ALFKI'";
                    SqlCommand updateCommand = new SqlCommand(updateQuery, connection);
                    int rowsAffected = updateCommand.ExecuteNonQuery();

                    Console.WriteLine($"Rows Affected: {rowsAffected}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine("An error occurred: " + ex.Message);
                }
                finally
                {
                    // 关闭数据库连接
                    connection.Close();
                }
            }

            Console.ReadLine();
        }
    }
}
```

在上面的示例代码中，我们首先定义了数据库连接字符串，其中包含了服务器名称、数据库名称、用户名和密码。然后，我们使用`SqlConnection`类创建了一个数据库连接对象，并将连接字符串传递给它。

在`try`块中，我们使用`Open()`方法打开数据库连接。然后，我们使用`SqlCommand`类创建了一个查询对象，并将查询字符串和数据库连接对象传递给它。我们使用`ExecuteReader()`方法执行查询，并使用`SqlDataReader`类读取查询结果。在`while`循环中，我们逐行读取查询结果，并将数据打印到控制台。

接下来，我们使用另一个`SqlCommand`对象执行了一个更新操作。我们使用`ExecuteNonQuery()`方法执行更新，并返回受影响的行数。最后，我们使用`Console.WriteLine()`打印出受影响的行数。

在`catch`块中，我们捕获并处理任何异常。在`finally`块中，我们使用`Close()`方法关闭数据库连接，确保在任何情况下都会关闭连接。

以上示例代码演示了如何使用C#连接并操作数据库。您可以根据自己的需求和数据库架构进行修改和扩展。



特别说明：：

```C#
/*
	SqlCommand类是C#中用来执行SQL语句的类
/*
```

