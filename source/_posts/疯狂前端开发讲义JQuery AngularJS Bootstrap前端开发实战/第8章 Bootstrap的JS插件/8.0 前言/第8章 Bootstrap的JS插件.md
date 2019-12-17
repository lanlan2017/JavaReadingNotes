---
title: 第8章 Bootstrap的JS插件
categories: 
  - 疯狂前端开发讲义JQuery AngularJS Bootstrap前端开发实战
  - 第8章 Bootstrap的JS插件
  - 8.0 前言
date: 2019-08-05 23:09:30
updated: 2019-11-25 11:30:20
abbrlink: '181137e2'
---
<div id='my_toc'><a href="/JavaReadingNotes/181137e2/#第8章-Bootstrap的JS插件" class="header_1">第8章 Bootstrap的JS插件</a><br><a href="/JavaReadingNotes/181137e2/#本章要点" class="header_2">本章要点</a><br></div>
<style>
    .header_1{
        margin-left: 1em;
    }
    .header_2{
        margin-left: 2em;
    }
    .header_3{
        margin-left: 3em;
    }
    .header_4{
        margin-left: 4em;
    }
    .header_5{
        margin-left: 5em;
    }
    .header_6{
        margin-left: 6em;
    }
</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}
var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}
</script>

<!--end-->
<!--SSTStart-->
# 第8章 Bootstrap的JS插件 #
## 本章要点 ##
- Bootstrap插件库概述与两种使用方式
- 掌握`对话框插件`的用法
- 掌握`下拉菜单`的用法
- 掌握`滚动监听插件`的功能和用法
- 掌握`标签页插件`的用法
- 掌握`胶囊式标签页`的用法
- 掌握`工具提示插件`的用法
- 掌握`弹出框插件`的功能和用法
- 掌握`警告框插件`的用法
- 掌握`按钮插件`的用法
- 掌握`折叠插件`的用法
- 利用折叠插件实现`手风琴效果`
- 掌握`轮播图插件`的功能和用法

虽然前面介绍`Bootstrap`主要是一个`CSS`框架,其提供了大量`CSS`样式供开发者使用,但它也提供了警告框等组件,这些组件也需要JS 脚本的支持。实际上,`Bootstrap`也提供了JS库,前面介绍`Bootstrap`安装时就介绍了必须在页面中添加`bootstrap.min.js`或`bootstrap.js`库,这两个库就是`Bootstrap`的JS库,这些JS库不仅负责为JS组件提供支持,也负责**提供系列内置的JS插件**。**本章将会详细介绍`Bootstrap`内置的系列JS插件的功能和用法**。
<!--SSTStop-->

