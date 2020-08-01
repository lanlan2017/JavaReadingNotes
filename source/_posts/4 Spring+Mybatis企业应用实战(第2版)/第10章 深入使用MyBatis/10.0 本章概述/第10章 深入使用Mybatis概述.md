---
title: 第10章 深入使用Mybatis概述
categories: 
  - 4 Spring+Mybatis企业应用实战(第2版)
  - 第10章 深入使用MyBatis
  - 10.0 本章概述
date: 2020-07-22 02:25:06
updated: 2020-07-22 02:26:33
abbrlink: 5cd614da
---
<div id='my_toc'><a href="/JavaReadingNotes/5cd614da/#第10章-深入使用Mybatis概述" class="header_1">第10章 深入使用Mybatis概述</a>&nbsp;<br><a href="/JavaReadingNotes/5cd614da/#本章要点" class="header_2">本章要点</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 第10章 深入使用Mybatis概述
## 本章要点
- 一对一映射 
- 一对多映射 
- 多对多映射 
- 动态SQL映射 
- 调用存储过程 
- 事务管理 
- 缓存机制

通过`MyBatis`的支持，应用程序可以从底层的`JDBC`中抽离出来，以面向对象的方式进行数据库访问。但面向对象远不止这些内容，比如对象和对象之间的关联关系，这对于客观世界的建模是非常重要的。本章将深入介绍`MyBatis`的关联映射，也会详细介绍`MyBatis`的动态`SQL`查询。
