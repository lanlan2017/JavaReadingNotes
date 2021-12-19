---
title: 第2章 JSP Servlet及相关技术详解 概述
categories: 
  - 2 轻量级Java EE企业应用实战(第5版)
  - 第2章 JSP Servlet及相关技术详解
  - 2.0 概述
date: 2020-06-05 03:56:40
updated: 2020-06-10 08:12:30
abbrlink: bc21eebe
---
# 第2章 JSP Servlet及相关技术详解 概述
## 本章要点
- `Web`应用的基本结构和`web.xml`文件
- `JSP`的基本原理
- `JSP`声明
- `JSP`注释和`HTML`注释
- `JSP`输出表达式
- `JsP`脚本
- `JSP`的3个编译指令
- `JSP`的7个动作指令
- `JSP`脚本中的9个内置对象
- `Servlet`的开发步骤
- 用`XML`或`Servlet3`的`Annotation`配置`Servlet`
- `Servlet`运行的生命周期
- `MVC`基础
- 开发`JSP2`自定义标签库
- 使用有属性的标签
- 使用带标签体的标签
- 开发、配置`Filter`以及`Filter`的功能
- 开发、配置`Listener`以及`Listener`的功能
- 配置`JSP`属性
- `JSP2`的表达式语言
- `JSP2`的`TagFile`标签库
- `Servlet3.1`的`web`模块部署描述符
- `Servlet3.1`提供的异步支持
- `Servlet3.1`增强的`ServletAPI`
- `Servlet3.1`提供的非阻塞`IO`
- `Tomcat8.5`的`WebSocket`支持

## 概述
`JSP( Java Server Page)`和`Servlet`是`JavaEE`规范的两个基本成员,它们是`Java Web`开发的重点知识,也是`JavaEE`开发的基础知识。`JSP`和`Servlet`的本质是一样的,因为`JSP`最终必须编译成`Servlet`才能运行,或者**说`JSP`只是生成`Servlet`的“草稿”文件**。
`JSP`比较简单,它的特点是在`HTML`页面中嵌入`Java`代码片段,或使用各种`JSP`标签,包括使用用户自定义标签,从而可以动态地提供页面内容。早期`JSP`页面的使用非常广泛,一个`Web`应用可以全部由`JSP`页面组成,只辅以少量的`JavaBean`即可。自`JavaEE`标准出现以后,人们逐渐认识到使用`JSP`充当过多的角色是不合适的。因此,`JSP`慢慢发展成单一的表现层技术,不再承担业务逻辑组件及持久层组件的责任。
随着`Java EE`技术的发展,又出现了`FreeMarker`、`Velocity`、`Tapestry`等表现层技术,虽然这些技术基本可以取代`JSP`技术,但实际上`JSP`依然是应用最广泛的表现层技术。本书介绍的`JSP`技术是基于`JSP2.3`、`Servlet3.1`规范的,因此请使用支持`JavaEE7`规范的应用服务器或支持`Servlet3.0`的`Web`服务器(比如`Tomcat8.5.X`)。
除了介绍`JSP`技术之外,本章也会讲解`JSP`的各种相关技术:`Servlet`、`Listener`、`Filter`以及自定义标签库等技术。
