---
title: 附录D 对象查询语言（OQL）简介[1]
categories: 
  - 9 深入理解Java虛拟机：JVM高级特性与最佳实践(第3版)
  - 6附录A 在Windows系统下编译OpenJDK 6
abbrlink: 830a477d
date: 2021-11-28 12:14:52
updated: 2021-11-28 12:14:52
---
# 附录D 对象查询语言（OQL）简介
[^1]
## D.1 SELECT子句
SELECT子句用于确定查询语句需要从堆转储快照中选择什么内容。如果需要显示堆转储快照中的对象，并且浏览这些对象的引用关系，可以使用“*”，这与传统SQL语句中的习惯是一致的，如：

```sql
SELECT * FROM java.lang.String
```
## 1.选择特定的显示列
查询也可以选择特定的需要显示的字段，如：

```
SELECT toString(s), s.count, s.value FROM java.lang.String s
```
查询可以通过“@”符号来使用Java对象的内存属性访问器。MAT提供了一系列的内置函数来获取与分析相关的信息，如：

```sql
SELECT toString(s), s.@usedHeapSize, s.@retainedHeapSize FROM java.lang.String s
```
关于对象属性访问器的具体内容，可以参见下文的“属性访问器”。

## 2.使用列别名
可以使用AS关键字来对选择的列进行命名，如：

```sql
SELECT toString(s) AS Value, 
    s.@usedHeapSize AS “Shallow Size”, 
    s.@retainedHeapSize AS “Retained Size” 
FROM java.lang.String s
```
可以使用AS RETAINED SET关键字来获得与选择对象相关联的对象集合，如：

```
SELECT AS RETAINED SET * FROM java.lang.String
```
## 3.拼合成为一个对象列表选择项目
可以使用OBJECTS关键字把SELECT子句中查找出来的数据项目转换为对象，如：

```
SELECT OBJECTS dominators(s) FROM java.lang.String s
```
上面例子中，dominators()函数将会返回一个对象数组，所以如果没有OBJECTS关键字，上面的查询将返回一组二维的对象数组的列表。通过使用关键字OBJECTS，迫使OQL把查询结果缩减为一维的对象列表。

## 4.排除重复对象
使用DISTINCT关键字可以排除结果集中的重复对象，如：

```
SELECT DISTINCT classof(s) FROM java.lang.String s
```
上面的例子中，classof()函数的作用是返回对象所属的Java类，当然，所有字符串对象的所属类都是java.lang.String，所以如果上面的查询中没有加入DISTINCT关键字，查询结果就会返回与快照中的字符串数量一样多的行记录，并且每行记录的内容都是java.lang.String类型。

## D.2 FROM子句
### 1.FROM子句指定需要查询的类
OQL查询需要在FROM子句定义的查询范围内进行操作。FROM子句可以接受的查询范围有下列几种描述方式：

（1）通过类名进行查询，如：
```
SELECT * FROM java.lang.String
```
（2）通过正则表达式匹配一组类名进行查询，如：
```
SELECT * FROM “java\.lang\..*”
```
（3）通过类对象在堆转储快照中的地址进行查询，如：
```
SELECT * FROM 0xe14a100
```
（4）通过对象在堆转储快照中的ID进行查询，如：
```
SELECT * FROM 3022
```
（5）在子查询中的结果集中进行查询，如：
```
SELECT * FROM (SELECT * FROM java.lang.Class c WHERE c implements org.eclipse.mat.snapshot.model.IClass) 
```
上面的查询返回堆转储快照中所有实现了org.eclipse.mat.snapshot.model.IClass接口的类。下面的这 句查询语句使用属性访问器达到了同样的效果，它直接调用了ISnapshot对象的方法：
```
SELECT * FROM $snapshot.getClasses()
```
### 2.包含子类
使用INSTANCEOF关键字把指定类的子类列入查询结果集之中，如：
```
SELECT * FROM INSTANCEOF java.lang.ref.Reference
```
这个查询的结果集中将会包含WeakReference、SoftReference和PhantomReference类型的对象，因为它们都继承自java.lang.ref.Reference。下面这句查询语句也有相同的结果：

```
SELECT * FROM $snapshot.getClassesByName(“java.lang.ref.Reference”, true)
```
## 3.禁止查询类实例
在FROM子句中使用OBJECTS关键字可以禁止OQL把查询的范围解释为对象实例，如：

```
SELECT * FROM OBJECTS java.lang.String
```
这个查询的结果不是返回快照中所有的字符串，而是只有一个对象，也就是与java.lang.String类对应的Class对象。

## D.3 WHERE子句
### 1.`>=，<=，>，<，[NOT]LIKE，[NOT]IN`（关系操作）
WHERE子句用于指定搜索的条件，即从查询结果中删除不需要的数据，如：

```sql
SELECT * FROM java.lang.String s WHERE s.count >= 100 
SELECT * FROM java.lang.String s WHERE toString(s) LIKE “.*day” 
SELECT * FROM java.lang.String s WHERE s.value NOT IN dominators(s)
```
### 2.`=，!=`（等于操作）
```
SELECT * FROM java.lang.String s WHERE toString(s) = “monday”
```

### 3.`AND`（条件与操作）
```
SELECT * FROM java.lang.String s WHERE s.count > 100 AND s.@retainedHeapSize > s.@usedHeapSize
```
### 4.`OR`（条件或操作）
“条件或操作”可以应用于表达式、常量文本和子查询之中，如：

```
SELECT * FROM java.lang.String s WHERE s.count > 1000 OR s.value.@length > 1000
```

### 5.文字表达式
文字表达式包括了布尔值、字符串、整型、长整型和null，如：

```
SELECT * FROM java.lang.String s 
    WHERE ( s.count > 1000 ) = true 
    WHERE toString(s) = “monday” 
    WHERE dominators(s).size() = 0 
    WHERE s.@retainedHeapSize > 1024L 
    WHERE s.@GCRootInfo != null
```
## D.4 属性访问器
### 1.访问堆转储快照中对象的字段
对象的内存属性可以通过传统的“点表示法”进行访问，格式为：

```
[<alias>.] <field>.<field>.<field>...
```
### 2.访问Java Bean属性
格式为：

```
[<alias>.] @<attribute> ...
```
使用@符号，OQL可以访问底层Java对象的内存属性。下表列出了一些常用的Java属性。

![image-20211127203831071](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211127203831.png)

### 3.调用OQLJava方法
格式为：
```
[<alias>.]@<方法>([<表达式>，<表达式>])...
```
加“()”会将MAT解释为一个OQLJava方法调用。这个方法的调用是通过反射执行的。常见的OQL Java方法如下：

![image-20211127203928619](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211127203928.png)

### 4.OQL的内建函数
格式为：
```
<function>(<parameter>)
```

![image-20211127204007219](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211127204007.png)

### D.5 OQL语言的BNF范式

![image-20211127204029605](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211127204029.png)

![image-20211127204041963](https://gitee.com/XiaoLan223/images/raw/master/Blog/Sum/20211127204042.png)

[^1]: 本文翻译自Eclipse Memory Analyzer Tool（MAT，Eclipse出品的内存分析工具）的OQL帮助文档。
