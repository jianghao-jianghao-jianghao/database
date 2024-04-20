#### 1.3.1 建立数据库对象

3．在数据库“订货”中，建立如表1-1、表1-2所示的数据库表：

```sql
CREATE TABLE 仓库 (
    仓库号 VARCHAR(50) PRIMARY KEY,
    城市 VARCHAR(50),
    面积 INT
);
```

```sqlite
CREATE TABLE 职工 (
    职工号 VARCHAR(50) PRIMARY KEY,
    仓库号 VARCHAR(50) REFERENCES 仓库(仓库号),
    工资 INT
);
```

4．向 “仓库”、“职工”表写入如表1-3、表1-4所示数据：

```sqlite
-- 向 "仓库" 表中写入数据
INSERT INTO 仓库 (仓库号, 城市, 面积) VALUES
('WH1', '北京', 370),
('WH2', '上海', 500),
('WH3', '广州', 200),
('WH4', '武汉', 400);

-- 向 "职工" 表中写入数据
INSERT INTO 职工 (仓库号, 职工号, 工资) VALUES
('WH2', 'E1', 1220),
('WH1', 'E3', 1210),
('WH2', 'E4', 1250),
('WH3', 'E6', 1230),
('WH1', 'E7', 1250);
```

#### 1.3.2 查询设计器使用

1．打开数据库SQL Server 2008 R2的查询设计器，用SQL语言建立如表1-5、表1-6所示数据库表，表结构如下图所示：

```sqlite
-- 创建供应商表
CREATE TABLE 供应商 (
    供应商号 VARCHAR(50) PRIMARY KEY,
    供应商名 VARCHAR(50),
    地址 VARCHAR(50)
);

-- 创建订购单表
CREATE TABLE 订购单 (
    订购单号 VARCHAR(50) PRIMARY KEY,
    供应商号 VARCHAR(50) REFERENCES 供应商(供应商号),
    职工号 VARCHAR(50) REFERENCES 职工(职工号),
    订购日期 DATETIME
);
```

2．用SQL语言向 “供应商”、“订购单”插入如表1-7、表1-8所示记录：

```sqlite
-- 向 "供应商" 表中插入数据
INSERT INTO 供应商 (供应商号, 供应商名, 地址) VALUES
('S3', '振华电子厂', '西安'),
('S4', '华通电子公司', '北京'),
('S6', '607厂', '郑州'),
('S7', '爱华电子厂', '北京');

-- 向 "订购单" 表中插入数据
INSERT INTO 订购单 (职工号, 供应商号, 订购单号, 订购日期) VALUES
('E3', 'S7', 'OR67', '2002-06-23 00:00:00'),
('E1', 'S4', 'OR73', '2002-07-28 00:00:00'),
('E7', 'S4', 'OR76', '2002-05-25 00:00:00'),
('E6', NULL, 'OR77', NULL),
('E3', 'S4', 'OR79', '2002-06-13 00:00:00'),
('E1', NULL, 'OR80', NULL),
('E3', NULL, 'OR90', NULL),
('E3', 'S3', 'OR91', '2002-07-13 00:00:00');

```

3.在查询设计器中完成以下简单查询。

以下是在查询设计器中完成简单查询的SQL语句：

1) 从职工关系中检索所有工资值：

```sql
SELECT 工资 FROM 职工;
```

2) 检索仓库关系中的所有元组：

```sql
SELECT * FROM 仓库;
```

3) 检索工资多于1230元的职工号：

```sql
SELECT 职工号 FROM 职工 WHERE 工资 > 1230;
```

4) 给出在仓库WH1或WH2工作，并且工资少于1250元的职工：

```sql
SELECT 职工号 FROM 职工 WHERE 仓库号 IN ('WH1', 'WH2') AND 工资 < 1250;
```



### 课外拓展

要打开 SQLite 文件，您可以使用 SQLite 数据库管理工具或者 SQLite 命令行工具。以下是一些常见的方法：

1. **SQLite 数据库管理工具：** 您可以使用像 DB Browser for SQLite 或 SQLiteStudio 这样的数据库管理工具来打开 SQLite 文件。这些工具提供了图形化界面，让您可以轻松地浏览、编辑和查询 SQLite 数据库。

2. **SQLite 命令行工具：** 您也可以使用 SQLite 提供的命令行工具来操作 SQLite 文件。您可以在命令行中输入 `sqlite3` 命令，然后指定要打开的 SQLite 文件的路径。这将会打开一个交互式的 SQLite Shell，允许您执行 SQL 查询和其他操作。

3. **应用程序集成：** 如果您的应用程序需要访问 SQLite 数据库文件，您可以通过编程语言的 SQLite 接口（如 Python 的 sqlite3 模块）来打开和操作 SQLite 文件。这样可以让您的应用程序直接与 SQLite 数据库进行交互。

无论您选择哪种方法，确保在打开 SQLite 文件之前备份您的数据，以防意外情况发生。
