---
title: SQL语句分类：DQL DML TPL DCL DDL CCL
categories:
  - 4 Spring+Mybatis企业应用实战(第2版)
  - 第9章 MyBatis的基本用法
  - 9.4 深入Mapper XML映射文件
abbrlink: '676e2053'
date: 2021-08-16 21:05:02
updated: 2021-08-16 21:05:02
---
# SQL语句结构

结构化查询语言包含6个部分：

## 一：数据查询语言（DQL:Data Query Language）：

其语句，也称为“数据检索语句”，用以从表中获得数据，确定数据怎样在应用程序给出。保留字`select`是`DQL`（也是所有`SQL`）用得最多的动词，其他`DQL`常用的保留字有`where`，`order by`，`group by`和`having`。这些`DQL`保留字常与其他类型的`SQL`语句一起使用。

## 二：数据操作语言（DML：Data Manipulation Language）：

其语句包括动词`insert`，`update`和`delete`。它们分别用于添加，修改和删除表中的行。也称为动作查询语言。

## 三：事务处理语言（TPL）：

它的语句能确保被`DML`语句影响的表的所有行及时得以更新。`TPL`语句包括`begin transaction`，`commit`和`rollback`。

## 四：数据控制语言（DCL）：

它的语句通过`grant`或`revoke`获得许可，确定单个用户和用户组对数据库对象的访问。某些`RDBMS`可用`grant`或`revoke`控制对表单个列的访问。

## 五：数据定义语言（DDL）：

其语句包括动词`create`和`drop`。在数据库中创建新表或删除表（`creat table`或`drop table`）；为表加入索引等。`DDL`包括许多与人数据库目录中获得数据有关的保留字。它也是动作查询的一部分。

## 六：指针控制语言（CCL）：

它的语句，像`declare cursor`，`fetch into`和`update where current`用于对一个或多个表单独行的操作。

# 参考资料
[https://www.w3cschool.cn/sql/](https://www.w3cschool.cn/sql/)