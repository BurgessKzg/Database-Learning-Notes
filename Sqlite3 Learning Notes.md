> &emsp;&emsp;基于嵌入式的数据库：Sqlite3。

# 1. 概念介绍

- **数据**
> &emsp;&emsp;能够输入计算机并能被计算机程序识别和处理的信息集合。

- **数据库**
> &emsp;&emsp;数据库是在数据库管理系统管理和控制之下，存放在存储介质上的数据集合。

# 2. 常用数据库

> &emsp;&emsp;多数数据库为关系型，关系型数据库是指：数据库管理系统内部在建立数据存储表格时，以数据与数据之间的逻辑关系为依据。

## 2.1. 小型数据库

- **Mysql**
> &emsp;&emsp;Mysql是一个小型关系型数据库管理系统。由瑞典Mysql-AB公司(2008年被sun公司收购,后sun公司又被Oracle公司收购)开发,源码开源，市场占有率可观，多应用于国内网站后台存储数据。

## 2.2. 中型数据库

- **Sql Server**
> &emsp;&emsp;微软开发的主要支持windows平台的数据库产品。

## 2.3. 大型数据库

- **Oracle**
> &emsp;&emsp;由Oracle公司开发的关系型数据库，支持多种操作系统，市场占有率最高。

- **DB2**
> &emsp;&emsp;由IBM公司开发的具备网上功能的多媒体关系数据库管理系统。

## 2.4. 嵌入式数据库

- **Sqlite**
> &emsp;&emsp;关系型数据库，支持ACID，占用资源少。

- **Firebird**
> &emsp;&emsp;关系型数据库，支持存储过程、兼容SQL。

- **eXtremeDB**
> &emsp;&emsp;内存数据库，运行效率高。

- **BerkeleyDB**
> &emsp;&emsp;没有数据库服务器概念，直接链接到应用程序中使用。

# 3. Sqlite

## 3.1. 简介

> &emsp;&emsp;Sqlite是一款轻量级嵌入式数据库，由C和C++语言编写完成，源代码开放。

- **特点：**
  - 占用资源少，全部代码大概2万行，250KB；
  - 最大支持2TB数据管理；
  - 数据操作较快；
  - 不需要安装和配置管理；
  - 兼容大小端，可以在不同字节序设备间自由共享；
  - 是一个存储在单一磁盘文件中的完整的数据库。

## 3.2. 安装

### 3.2.1. 在线安装

- 终端命令行：`sudo apt-get install sqlite3`

### 3.2.2. 本地安装

- 1. 需要准备三个deb包：
  - libsqlite3-0_3.22.0-1ubuntu0.1_i386.deb
  - libsqlite3-dev_3.22.0-1ubuntu0.1_i386.deb
  - sqlite3_3.22.0-1ubuntu0.1_i386.deb
- 2. 终端命令行执行：`sudo dpkg -i *.deb`；
- 3. 在终端命令行输入：`sqlite3`就可以进入数据库管理系统；

# 4. Sqlite基本命令

> Sqlite命令有两种类型：
>   - 以"."开头的是系统命令；
>   - 不以"."开头的是sql命令，需要以";"结尾；

## 4.1. 创建数据库

- 格式：`sqlite3 Test.db`；
- 解释：创建一个名为"Test"的数据库，数据库后缀为".db"；

## 4.2. 系统命令

### 4.2.1. ".help"命令

> 帮助

### 4.2.2. ".quit"命令

> 退出

### 4.2.3. ".exit"命令

> 退出

### 4.2.4. ".schema"命令

> 查看表格的结构图；

### 4.2.5. ".database"命令

> 查看打开的数据库，包括名字和路径；

### 4.2.6. ".table"命令

> 查看当前打开的数据库中的表格；

## 4.3. sql命令

### 4.3.1. 创建表格

**格式：`create table stu(id Integer,name char,score float);`**
**格式：`create table stu(id integer,name string,score float);`**
  - 创建一张名为"stu"的表格；
  - sql命令需要以";"结尾；
  - 表格中有Integer类型的id字段；
  - 表格中有char类型的name字段(char、string都可以)；

### 4.3.2. 插入记录

**格式：`insert into stu VALUES (001,"张三",80);`** 
**格式：`insert into stu VALUES (002,'李四',90);`**
**格式：`insert into stu (id,score)VALUES (003,95);`** 
**格式：`insert into stu (name,score)VALUES (98,'马六');`** 
  - 向表格"stu"中插入一条记录；
  - 字符串可以使用单引号(')或双引号(")括起来；
  - 某条记录只插入部分字段时，需要在"values"关键字前指定插入哪些字段；
  - 指定字段和插入数据类型不匹配值会错误插入，sqlite不会做类型检查；

### 4.3.3. 查询记录

**格式：`select * from stu;`**
**格式：`select name from stu;`**
**格式：`select id,score from stu;`**
**格式：`SELECT * from stu where id = 1;`**
**格式：`SELECT * from stu where id=2 and name = '李四';`**
  - "*"代表查看全部字段；
  - 也可以指定查看部分字段；
  - 支持条件查询，使用关键字：where；
  - 多条件查询，条件之间可用关键字：and/AND、or/OR

    ```SQL
      sqlite> select * from stu;
      1|张三|80.0
      2|李四|90.0
      3||95.0
      |98|马六
      sqlite> select score from stu;
      80.0
      90.0
      95.0
      马六
      sqlite> SELECT id,score from stu;
      1|80.0
      2|90.0
      3|95.0
      |马六
      sqlite> SELECT * from stu where id = 1;
      1|张三|80.0
      sqlite> SELECT * from stu where id=1;
      1|张三|80.0
      sqlite> SELECT * from stu where id=2 and name = '张三';
      sqlite> SELECT * from stu where id=2 and name = '李四';
      2|李四|90.0
      sqlite>
    ```

### 4.3.4. 删除记录

**格式：`delete from stu;`**
**格式：`delete from stu where id=001;`**
  - 不加条件判断，会删除整个表格；
  - 可以使用关键字：AND、OR来确定要删除的记录；

    ```SQL
      sqlite> SELECT * from stu;
      1|zhangsan|80.0
      2|王五|66.0
      3||95.0
      |98|马六
      sqlite> DELETE from stu where id= 3;
      sqlite> SELECT * from stu;
      1|zhangsan|80.0
      2|王五|66.0
      |98|马六
      sqlite> DELETE from stu;
      sqlite> SELECT * from stu;
      sqlite> 
    ```

### 4.3.5. 更新记录

**格式：`update stu set name='zhangsan' where id =01;`**
**格式：`update stu set name='王五',score = 66 where id =2;`**
  - 通过条件可以更新指定记录；
  - 可以更新记录的多个字段；

    ```SQL
      sqlite> SELECT * from stu;
      1|张三|80.0
      2|李四|90.0
      3||95.0
      |98|马六
      sqlite> update stu set name='zhangsan' where id =01;
      sqlite> SELECT * from stu;
      1|zhangsan|80.0
      2|李四|90.0
      3||95.0
      |98|马六
      sqlite> update stu set name='王五',score = 66 where id =2;
      sqlite> SELECT * from stu;
      1|zhangsan|80.0
      2|王五|66.0
      3||95.0
      |98|马六
      sqlite> 
    ```

### 4.3.6. 添加字段

**格式：`alter table stu add column address char`**
  - 向表格stu中添加一个名称为"address"，类型为char的字段(列)；

### 4.3.7. 删除表格

**表格：`drop table stu`**
  - 删除名字为"stu"的表格；

### 4.3.8. 删除字段

**顺序1：`CREATE TABLE stuTemp as SELECT id,name from stu;`**
**顺序2：`drop TABLE stu;`**
**顺序3：`alter TABLE stuTemp RENAME to stu;`**
- sqlite不支持直接删除一列，可以通过以下方式实现删除一列：
  - 1.创建一张新的表；
  - 2.删除原有的表；
  - 3.将新表的名字改为原有的表的名字；

    ```SQL
      sqlite> select * FROM stu;
      1|张三|60.0
      2|李四|70.0
      sqlite> CREATE TABLE stuTemp as SELECT id,name from stu;
      sqlite> SELECT * from stuTemp;
      1|张三
      2|李四
      sqlite> drop TABLE stu;
      sqlite> alter TABLE stuTemp RENAME to stu;
      sqlite> .schema
      CREATE TABLE IF NOT EXISTS "stu"(id INT,name NUM);
      sqlite> .table
      stu
    ```

# 5. Sqlite编程接口

---

**链接**
[官方链接](https://www.sqlite.org/c3ref/funclist.html)
[菜鸟教程](https://www.runoob.com/sqlite/sqlite-tutorial.html)

---

- sqlite3_open
- sqlite3_close
- sqlite3_errmsg
- sqlite3_exec

---

- sqlite3_get_table使用之后，需要释放table的空间？
- sqlite_open为什么要使用一个二级指针？
- UIF-8格式？还有哪些？
- sqlite_errmsg函数返回字符串首地址是怎么实现？不会造成内存泄漏？strerror函数呢？某些返回结构体指针的函数内部怎么实现？
  - 1. 直接返回结构体，这种方式只是返回局部变量的一个拷贝。
  - 2. 可以在函数体内用new 一个结构体，然后返回它的指针，之后在外部对这块内存进行管理。
  - 3. 使用引用参数，如3楼所说，这种方式会显得比较有好，比起第二种对内存管理要方便些
- 字符串常量存放在程序的静态数据区，那静态数据区是否占用内存，过多的定义字符串常量是不是很浪费内存？
  ```C
    const char* Func(void)
    {
        const char* p = "hello world";//字符串常量存放在程序的静态数据区
        return p;
    }
  ```


