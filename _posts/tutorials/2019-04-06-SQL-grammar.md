---
layout: post
title: SQL语法基础篇
date: 2019-04-06 20:49:52 +0800
categories: SQL
tag: note
---

* content
{:toc}


# 概述

## 数据库表

一个数据库通常包含一个或多个表。每个表由一个名字标识（例如“客户”或者“订单”）。表包含带有数据的记录（行）。

下面的例子是一个名为 "Persons" 的表：

Id|LastName|FirstName|Address|City
-|-|-|-|-
1|Adams|John|Oxford Street|London
2|Bush|George|Fifth Avenue|New York
3|Carter|Thomas|Changan Street|Beijing

上面的表包含三条记录（每一条对应一个人）和五个列（Id、姓、名、地址和城市）。

## SQL语法

可以把 SQL 分为两个部分：数据操作语言 (DML) 和 数据定义语言 (DDL)。

查询和更新指令构成了 DML 语句：

* SELECT - 从数据库表中获取数据
* UPDATE - 更新数据库表中的数据
* DELETE - 从数据库表中删除数据
* INSERT INTO - 向数据库表中插入数据

SQL 的数据定义语言 (DDL) 使我们有能力创建或删除表格。我们也可以定义索引（键），规定表之间的链接，以及施加表间的约束。

SQL 中最重要的 DDL 语句:

* CREATE DATABASE - 创建新数据库
* ALTER DATABASE - 修改数据库
* CREATE TABLE - 创建新表
* ALTER TABLE - 变更（改变）数据库表
* DROP TABLE - 删除表
* CREATE INDEX - 创建索引（搜索键）
* DROP INDEX - 删除索引

**注：SQL语句对大小写不敏感。** 

## SQL语句后面的分号

分号是在数据库系统中分隔每条 SQL 语句的标准方法，这样就可以在对服务器的相同请求中执行一条以上的语句。

如果是 MS Access 和 SQL Server 2000，则不必在每条 SQL 语句之后使用分号，不过某些数据库软件要求必须使用分号。

# SQL常用语句

## SELECT

### 语法

**SELECT 语句用于从表中选取数据。** 结果被存储在一个结果表中（称为结果集）。

```SQL
SELECT 列名称 FROM 表名称
SELECT * FROM 表名称
```

### 实例

1. 获取名为 "LastName" 和 "FirstName" 的列的内容（从名为 "Persons" 的数据库表）：

```SQL
SELECT LastName,FirstName FROM Persons
```

"Persons" 表:
|Id|LastName|FirstName|Address|City|
|-|-|-|-|-|
|1|Adams|John|Oxford Street|London|
|2|Bush|George|Fifth Avenue|New York|
|3|Carter|Thomas|Changan Street|Beijing|  

结果：
| LastName | FirstName |
| -------- | --------- |
| Adams    | John      |
| Bush     | George    |
| Carter   | Thomas    |

2. 从 Persons 表中选取所有的列：

```SQL
SELECT * FROM Persons
```

结果：
| Id  | LastName | FirstName | Address        | City     |
| --- | -------- | --------- | -------------- | -------- |
| 1   | Adams    | John      | Oxford Street  | London   |
| 2   | Bush     | George    | Fifth Avenue   | New York |
| 3   | Carter   | Thomas    | Changan Street | Beijing  |

## DISTINCT

### 语法

**关键词 DISTINCT 用于返回唯一不同的值。** 在表中，可能会包含重复值，有时也许希望仅仅列出不同（distinct）的值。

```SQL
SELECT DISTINCT 列名称 FROM 表名称
```

### 实例

Orders表：
| Company  | OrderNumber |
| -------- | ----------- |
| IBM      | 3532        |
| W3School | 2356        |
| Apple    | 4698        |
| W3School | 6953        |

如果要从 "Company" 列中选取所有的值，我们需要使用 SELECT 语句：

```SQL
SELECT Company FROM Orders
```

结果：
|Company|
|-|
|IBM|
|W3School|
|Apple|
|W3School|

注意，在结果集中W3School被列出了两次。

如需从 Company" 列中仅选取唯一不同的值，我们需要使用 SELECT DISTINCT 语句：

```SQL
SELECT DISTINCT Company FROM Orders
```

结果：
|Company
|-
|IBM
|W3School
|Apple

现在，在结果集中，"W3School" 仅被列出了一次。

## WHERE

### 语法

**WHERE 子句用于规定选择的标准。** 如需有条件地从表中选取数据，可将 WHERE 子句添加到 SELECT 语句。

```SQL
SELECT 列名称 FROM 表名称 WHERE 列+运算符+值
```

下面的运算符可在 WHERE 子句中使用：

| 操作符  | 描述         |
| ------- | ------------ |
| =       | 等于         |
| <>      | 不等于       |
| >       | 大于         |
| <       | 小于         |
| >=      | 大于等于     |
| <=      | 小于等于     |
| BETWEEN | 在某个范围内 |
| LIKE    | 搜索某种模式 |

**注**：在某些版本的 SQL 中，操作符 <> 可以写为 !=。

### 实例

如果只希望选取居住在城市 "Beijing" 中的人，我们需要向 SELECT 语句添加 WHERE 子句：

```SQL
SELECT * FROM Persons WHERE City='Beijing'
```

"Persons" 表
| LastName | FirstName | Address        | City     | Year |
| -------- | --------- | -------------- | -------- | ---- |
| Adams    | John      | Oxford Street  | London   | 1970 |
| Bush     | George    | Fifth Avenue   | New York | 1975 |
| Carter   | Thomas    | Changan Street | Beijing  | 1980 |
| Gates    | Bill      | Xuanwumen 10   | Beijing  | 1985 |

结果：
| LastName | FirstName | Address        | City    | Year |
| -------- | --------- | -------------- | ------- | ---- |
| Carter   | Thomas    | Changan Street | Beijing | 1980 |
| Gates    | Bill      | Xuanwumen 10   | Beijing | 1985 |

**注**：SQL 使用单引号来环绕**文本值**（大部分数据库系统也接受双引号）。如果是**数值**，请不要使用引号。

## AND & OR

### 语法

**AND 和 OR 运算符用于基于一个以上的条件对记录进行过滤。** AND 和 OR 可在 WHERE 子语句中把两个或多个条件结合起来。

### 实例

Persons 表
| LastName | FirstName | Address        | City     |
| -------- | --------- | -------------- | -------- |
| Adams    | John      | Oxford Street  | London   |
| Bush     | George    | Fifth Avenue   | New York |
| Carter   | Thomas    | Changan Street | Beijing  |
| Carter   | William   | Xuanwumen 10   | Beijing  |

1. 使用 AND 来显示所有姓为 "Carter" 并且名为 "Thomas" 的人：

```SQL
SELECT * FROM Persons WHERE FirstName='Thomas' AND LastName='Carter'
```

结果：
|LastName|FirstName|Address|City|
|-|-|-|-|
|Carter|Thomas|Changan Street|Beijing|

2. 使用 OR 来显示所有姓为 "Carter" 或者名为 "Thomas" 的人：

```SQL
SELECT * FROM Persons WHERE firstname='Thomas' OR lastname='Carter'
```

结果：
| LastName | FirstName | Address | City |
|-|-|-|-|
| Carter      |  Thomas        |  Changan Street  |  Beijing | |
| Carter      |  William      |  Xuanwumen 10      |  Beijing |

3. 我们也可以把 AND 和 OR 结合起来（使用圆括号来组成复杂的表达式）:

```SQL
SELECT * FROM Persons WHERE (FirstName='Thomas' OR FirstName='William')
AND LastName='Carter'
```

结果：
| LastName  |  FirstName  |  Address  |  City  |
| --------- |  ---------- | --------- | ------ |
| Carter    |  Thomas     |  Changan Street  |  Beijing |
| Carter   | William   | Xuanwumen 10   | Beijing |

## ORDER BY

### 语法

**ORDER BY 语句用于对结果集进行排序。** ORDER BY 语句默认按照升序对记录进行排序，可以使用 DESC 关键字进行降序排序。

### 实例

Orders 表：
| Company  | OrderNumber |
| -------- | ----------- |
| IBM      | 3532        |
| W3School | 2356        |
| Apple    | 4698        |
| W3School | 6953        |

1. 以字母顺序显示公司名称：

```SQL
SELECT Company, OrderNumber FROM Orders ORDER BY Company
```

结果：
| Company  | OrderNumber |
| -------- | ----------- |
| Apple    | 4698        |
| IBM      | 3532        |
| W3School | 6953        |
| W3School | 2356        |

2. 以字母顺序显示公司名称（Company），并以数字顺序显示顺序号（OrderNumber）：

```SQL
SELECT Company, OrderNumber FROM Orders ORDER BY Company, OrderNumber
```

结果：
| Company  | OrderNumber |
| -------- | ----------- |
| Apple    | 4698        |
| IBM      | 3532        |
| W3School | 2356        |
| W3School | 6953        |

3. 以逆字母顺序显示公司名称：

```SQL
SELECT Company, OrderNumber FROM Orders ORDER BY Company DESC
```

结果：
| Company  | OrderNumber |
| -------- | ----------- |
| W3School | 6953        |
| W3School | 2356        |
| IBM      | 3532        |
| Apple    | 4698        |

4. 以逆字母顺序显示公司名称，并以数字顺序显示顺序号：

```SQL
SELECT Company, OrderNumber FROM Orders ORDER BY Company DESC, OrderNumber ASC
```

结果：
| Company  | OrderNumber |
| -------- | ----------- |
| W3School | 2356        |
| W3School | 6953        |
| IBM      | 3532        |
| Apple    | 4698        |

## INSERT INTO

### 语法

**INSERT INTO 语句用于向表格中插入新的行。** 

```SQL
INSERT INTO 表名称 VALUES (值1, 值2,....)
```

我们也可以指定所要插入数据的列：

```SQL
INSERT INTO table_name (列1, 列2,...) VALUES (值1, 值2,....)
```

### 实例

"Persons" 表：
| LastName | FirstName | Address        | City    |
| -------- | --------- | -------------- | ------- |
| Carter   | Thomas    | Changan Street | Beijing |

1. 插入新的行

```SQL
INSERT INTO Persons VALUES ('Gates', 'Bill', 'Xuanwumen 10', 'Beijing')
```

结果：
| LastName | FirstName | Address        | City    |
| -------- | --------- | -------------- | ------- |
| Carter   | Thomas    | Changan Street | Beijing |
| Gates    | Bill      | Xuanwumen 10   | Beijing |

2. 在指定的列中插入数据

```SQL
INSERT INTO Persons (LastName, Address) VALUES ('Wilson', 'Champs-Elysees')
```

结果：
| LastName | FirstName | Address        | City    |
| -------- | --------- | -------------- | ------- |
| Carter   | Thomas    | Changan Street | Beijing |
| Gates    | Bill      | Xuanwumen 10   | Beijing |
| Wilson   |           | Champs-Elysees |

## UPDATE

### 语法

**Update 语句用于修改表中的数据。** 

```SQL
UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
```

### 实例

Person:
| LastName | FirstName | Address | City |
| --- | -------- | --------- | ------- |
| Gates    |  Bill     |  Xuanwumen 10 |  Beijing |
| Wilson   |           | Champs-Elysees |

1. 更新某一行中的一个列。我们为 LastName 是 "Wilson" 的人添加 FirstName：

```SQL
UPDATE Person SET FirstName = 'Fred' WHERE LastName = 'Wilson'
```

结果：
| LastName | FirstName | Address        | City    |
| -------- | --------- | -------------- | ------- |
| Gates    | Bill      | Xuanwumen 10   | Beijing |
| Wilson   | Fred      | Champs-Elysees |

2. 更新某一行中的若干列。修改地址（address），并添加城市名称（city）：

```SQL
UPDATE Person SET Address = 'Zhongshan 23', City = 'Nanjing'
WHERE LastName = 'Wilson'
```

结果：
| LastName | FirstName | Address | City |
| -------- | --------- | ------- |----- |
| Gates |  Bill |  Xuanwumen 10  |  Beijing |
| Wilson |  Fred |  Zhongshan 23  |  Nanjing |

## DELETE

### 语法

**DELETE 语句用于删除表中的行。**

```SQL
DELETE FROM 表名称 WHERE 列名称 = 值
```

### 实例

Person:
| LastName | FirstName | Address | City |  
|-|-|-|-|
| Gates        |  Bill            |  Xuanwumen 10  |  Beijing |
| Wilson   | Fred      | Zhongshan 23 | Nanjing |

1. 删除某行。删除"Fred Wilson" ：

```SQL
DELETE FROM Person WHERE LastName = 'Wilson' 
```

结果:
| LastName | FirstName | Address      | City    |
| -------- | --------- | ------------ | ------- |
| Gates    | Bill      | Xuanwumen 10 | Beijing |

2. 删除所有行。可以在不删除表的情况下删除所有的行，表的结构、属性和索引都是完整的：

```SQL
DELETE FROM table_name
DELETE * FROM table_name
```
