---
title: 示例 @CrossOrigin注解的使用
categories: 
  - Spring+Mybatis企业应用实战(第2版)
  - 第3章 Spring MVC的常用注解
  - 3.6 @CrossOrigin注解
date: 2019-08-19 16:49:35
updated: 2019-12-23 12:01:12
abbrlink: 559cdc31
---
<div id='my_toc'><a href="/JavaReadingNotes/559cdc31/#示例-@CrossOrigin注解的使用" class="header_1">示例 @CrossOrigin注解的使用</a>&nbsp;<br><a href="/JavaReadingNotes/559cdc31/#总结" class="header_2">总结</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
<!--SSTStart-->
# 示例 @CrossOrigin注解的使用
接下来测试跨域发送请求,再新建一个项目`CrossOriginTest`,加入所需的`jar`文件.
## 项目结构

<details><summary>展开/折叠</summary>

```
G:\Desktop\随书源码\Spring+Mybatis企业应用实战(第2版)\codes\03\CrossOriginTest
├─src\
│ └─org\
│   └─fkit\
│     └─controller\
│       └─CrossOriginController.java
└─WebContent\
  ├─META-INF\
  │ └─MANIFEST.MF
  └─WEB-INF\
    ├─content\
    │ └─welcome.jsp
    ├─lib\
    │ ├─commons-logging-1.2.jar
    │ ├─spring-aop-5.0.1.RELEASE.jar
    │ ├─spring-aspects-5.0.1.RELEASE.jar
    │ ├─spring-beans-5.0.1.RELEASE.jar
    │ ├─spring-context-5.0.1.RELEASE.jar
    │ ├─spring-context-indexer-5.0.1.RELEASE.jar
    │ ├─spring-context-support-5.0.1.RELEASE.jar
    │ ├─spring-core-5.0.1.RELEASE.jar
    │ ├─spring-expression-5.0.1.RELEASE.jar
    │ ├─spring-instrument-5.0.1.RELEASE.jar
    │ ├─spring-jcl-5.0.1.RELEASE.jar
    │ ├─spring-jdbc-5.0.1.RELEASE.jar
    │ ├─spring-jms-5.0.1.RELEASE.jar
    │ ├─spring-messaging-5.0.1.RELEASE.jar
    │ ├─spring-orm-5.0.1.RELEASE.jar
    │ ├─spring-oxm-5.0.1.RELEASE.jar
    │ ├─spring-test-5.0.1.RELEASE.jar
    │ ├─spring-tx-5.0.1.RELEASE.jar
    │ ├─spring-web-5.0.1.RELEASE.jar
    │ ├─spring-webflux-5.0.1.RELEASE.jar
    │ ├─spring-webmvc-5.0.1.RELEASE.jar
    │ └─spring-websocket-5.0.1.RELEASE.jar
    ├─springmvc-config.xml
    └─web.xml

```

</details>

## CrossOriginController.java
```java
package org.fkit.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;

// 允许所有域发送过来的请求
@CrossOrigin(maxAge = 3600)
@Controller
public class CrossOriginController
{
    // 只允许origins属性中指定的域的请求
    @CrossOrigin(origins = "http://localhost:8080/VariableTest")
    @GetMapping(value = "/welcome")
    public String welcome()
    {
        System.out.println("处理跨域请求");
        return "welcome";
    }
}
```
`CrossOriginController`类和`welcome`方法上都使用了`@CrossOrigin`注解。 `welcome`方法接收到`跨域请求`进行简单处理后,跳转到`welcome.jsp`。
## welcome.jsp
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>测试@CrossOrigin注解</title>
</head>
<body>
    <br>恭喜您，测试跨域访问成功!
</body>
</html>
```
此外,还需要在`web.xml`文件中配置`Spring MVC`的前端控制器`DispatcherServlet`,因为每次配置基本一致,此处不再赘述,读者可自行配置。
## 部署测试
同时部署`VariableTest`和`CrossOriginTest`两个`Web`应用,在浏览器中输入如下`URL`来测试进入`VariableTest`应用:
```
http://localhost:8080/VariableTest/
```
然后点击`测试@CrossOrigin注解`超链接:
```html
<!-- 跨域请求 -->
<a href="http://localhost:8080/CrossOriginTest/welcome">测试@CrossOrigin注解</a>
```
向另一个`Web`应用`CrossOriginTest`发送跨域请求,`CrossOriginTest`应用的`CrossOriginController`控制器的`welcome`方法将会处理这个跨域请求,控制台输出结果如下:
```
处理跨域请求
```
同时浏览器上将显示`CrossOriginTest`应用的`welcome.jsp`页面。

## 总结
`@CrossOrigin`注解可以接收从另一个`Web`应用发来的跨域请求。
<!--SSTStop-->