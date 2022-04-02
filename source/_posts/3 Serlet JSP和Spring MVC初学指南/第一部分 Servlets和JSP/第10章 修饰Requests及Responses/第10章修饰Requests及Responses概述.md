---
title: 第10章修饰Requests及Responses概述
categories: 
  - 3 Serlet JSP和Spring MVC初学指南
  - 第一部分 Servlets和JSP
  - 第10章 修饰Requests及Responses
abbrlink: 318f3b47
date: 2019-04-19 09:10:09
updated: 2022-04-03 01:21:16
---
# 第10章修饰Requests及Responses概述 #
`Servlet API`包含4个可修饰的类，用于改变`ServletRequest`以及`Servlet Response`。这种修饰允许**修改**`ServletRequest`以及`ServletResponse`或者`HTTP`中的等价类（即`HttpServletRequest`和`HttpServletResponse`）中的**任务方法**。这种修饰遵循`Decorator`模式或者`Wrapper`模式，因此在使用修饰前，需要了解一下该模式的内容。

本章从解释`Decorator`模式开始，说明如何通过修饰`HttpServletRequest`来修改`HttpServletRequest`对象的行为。该技术同样适用于修饰`HttpServletResponse`对象。
