---
title: 第11章 MyBatis的注解配置
categories: 
  - Spring+Mybatis企业应用实战(第2版)
  - 第11章 MyBatis的注解配置
date: 2019-06-13 18:29:24
updated: 2019-12-22 08:26:34
abbrlink: 408525dd
---
<div id='my_toc'><a href="/JavaReadingNotes/408525dd/#第11章-MyBatis的注解配置" class="header_1">第11章 MyBatis的注解配置</a><br><a href="/JavaReadingNotes/408525dd/#本章要点" class="header_2">本章要点</a><br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
# 第11章 MyBatis的注解配置 #
## 本章要点 ##
- `MyBatis`注解插入、修改、删除和査询操作.
- `MyBatis`注解一对对多和多对多操作.
- `MyBatis`注解动态`SQL`.
- `MyBatis`注解调用存储过程.
- `MyBatis`注解使用二级缓存.
前面的章节介绍了`MyBatis`的基本用法、关联映射、动态`SQL`和缓存机制等知识,其所有的配置都使用`XML`完成,但是大量的`XML`配置文件的编写是非常烦琐的,因此`MyBatis`也提供了更加简便的基于注解(`annotation`)的配置方式。本章将重点介绍`MyBatis`的注解配置.

