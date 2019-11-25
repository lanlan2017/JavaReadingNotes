---
title: 第17章 SpringMVC介绍
categories: 
  - Serlet JSP和Spring MVC初学指南
  - 第二部分 SpringMVC
  - 第17章 SpringMVC介绍
date: 2019-05-15 11:17:33
updated: 2019-11-02 10:12:05
abbrlink: 489657c9
---
<div id='my_toc'>

- [第17章 SpringMVC介绍](/JavaReadingNotes/489657c9/#第17章-SpringMVC介绍)

</div>
<!--more-->
<script>if (navigator.platform.toLowerCase() == 'win32'){document.getElementById('my_toc').style.display = 'none';}</script>

<!--end-->
# 第17章 SpringMVC介绍 #
第16章中，我们学习了现代`Web`应用程序广泛使用的`MVC`设计模式，也学习了模型2架构的优势以及如何构建一个模型2应用。`Spring MVC`框架可以帮助开发人员快速地开发`MVC`应用。
本章首先介绍采用`Spring MVC`的好处，以及`SpringMVC`如何加速模型2应用的开发。然后介绍`Spring MVC`的基本组件，包括`Dispatcher Servlet`，并学习如何开发一个“传统风格”的控制器，这是在`Spring 2.5`版本前开发`controller`的唯一方式。另一种方式将在第18章“基于注解的控制器”中介绍。之所以介绍传统方式，是因为我们可能不得不在基于旧版`Spring`的遗留代码上工作。对于新应用，我们可以采用基于注解的控制器。
此外，本章还会介绍`Spring MVC`配置，大部分的`Spring MVC`应用会用一个`XML`文档来定义应用中所用的`bean`。

