---
title: 示例 自定义HttpMessageConverter返回JSON格式的数据
categories: 
  - 4 Spring+Mybatis企业应用实战(第2版)
  - 第3章 Spring MVC的常用注解
  - 3.14 @ResponseBody注解
date: 2019-08-20 21:55:02
updated: 2020-05-10 02:21:31
abbrlink: 830b4262
---
<div id='my_toc'><a href="/JavaReadingNotes/830b4262/#示例-自定义HttpMessageConverter返回JSON格式的数据" class="header_1">示例 自定义HttpMessageConverter返回JSON格式的数据</a>&nbsp;<br><a href="/JavaReadingNotes/830b4262/#项目结构" class="header_2">项目结构</a>&nbsp;<br><a href="/JavaReadingNotes/830b4262/#index-jsp" class="header_2">index.jsp</a>&nbsp;<br><a href="/JavaReadingNotes/830b4262/#BookController-java" class="header_2">BookController.java</a>&nbsp;<br><a href="/JavaReadingNotes/830b4262/#springmvc-config-xml" class="header_2">springmvc-config.xml</a>&nbsp;<br></div>
<style>.header_1{margin-left: 1em;}.header_2{margin-left: 2em;}.header_3{margin-left: 3em;}.header_4{margin-left: 4em;}.header_5{margin-left: 5em;}.header_6{margin-left: 6em;}</style>
<!--more-->
<script>if (navigator.platform.search('arm')==-1){document.getElementById('my_toc').style.display = 'none';}var e,p = document.getElementsByTagName('p');while (p.length>0) {e = p[0];e.parentElement.removeChild(e);}</script>

<!--end-->
<!--SSTStart-->
# 示例 自定义HttpMessageConverter返回JSON格式的数据
接下来,使用`Fastjson`来返回`JSON`数据。
创建一个`Fastjson2Test`项目,在`WebContent`目录下创建一个`js`目录,加入`jQuery`和`json2`的`js`文件,在`WEB-INF/lib`目录中加入`Fastjson`的`jar`文件。
`Fastjson2Test`项目的所有`JSP`和`Java`文件和`ResponseBodyTest`一致,只是在`springmvc-config.xml`中使用了`Fastjson`的`FastJsonHttpMessageConverter`。读者可参考配套资源文件中对应的代码,测试结果和`ResponseBodyTest`项目一致,此处不再赘述.
## 项目结构
<details><summary>展开/折叠</summary><pre>
G:\Desktop\随书源码\Spring+Mybatis企业应用实战(第2版)\codes\03\Fastjson2Test
├─src\
│ └─org\
│   └─fkit\
│     ├─controller\
│     │ └─<a href="#BookController-java">BookController.java</a>
│     └─domain\
│       └─Book.java
└─WebContent\
  ├─<a href="#index-jsp">index.jsp</a>
  ├─js\
  │ ├─jquery-1.11.0.min.js
  │ ├─jquery-migrate-1.2.1.min.js
  │ └─json2.js
  ├─META-INF\
  │ └─MANIFEST.MF
  └─WEB-INF\
    ├─lib\
    │ ├─commons-logging-1.2.jar
    │ ├─<mark>fastjson-1.2.9.jar</mark>
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

</pre></details>

## index.jsp
```java
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>测试返回JSON格式的数据</title>
<script type="text/javascript" src="js/jquery-1.11.0.min.js"></script>
<script type="text/javascript" src="js/json2.js"></script>
<script type="text/javascript">
    $(document).ready(function() {
        testResponseBody();
    });
    function testResponseBody() {
        $.post("${pageContext.request.contextPath}/json/testRequestBody", null,
                function(data) {
                    $.each(data, function() {
                        var tr = $("<tr align='center'/>");
                        $("<td/>").html(this.id).appendTo(tr);
                        $("<td/>").html(this.name).appendTo(tr);
                        $("<td/>").html(this.author).appendTo(tr);
                        $("#booktable").append(tr);
                    })
                }, "json");
    }
</script>
</head>
<body>
    <table id="booktable" border="1" style="border-collapse: collapse;">
        <tr align="center">
            <th>编号</th>
            <th>书名</th>
            <th>作者</th>
        </tr>
    </table>
</body>
</html>
```
## BookController.java
```java
package org.fkit.controller;

import java.util.ArrayList;
import java.util.List;
import org.fkit.domain.Book;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
@RequestMapping(
    "/json"
)
public class BookController
{
    @RequestMapping(
        value = "/testRequestBody"
    )
    // @ResponseBody注解会自动将集合数据转换json格式并返回给客户端
    @ResponseBody
    public Object getJson()
    {
        List<Book> list = new ArrayList<Book>();
        list.add(new Book(1, "Spring+MyBatis企业应用实战", "肖文吉"));
        list.add(new Book(2, "轻量级JavaEE企业应用实战", "李刚"));
        return list;
    }
}
```
## springmvc-config.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:p="http://www.springframework.org/schema/p"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xsi:schemaLocation="http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc-4.3.xsd
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans-3.2.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context-4.3.xsd">
    <!-- spring可以自动去扫描base-pack下面的包或者子包下面的java文件， -->
    <!-- 如果扫描到有Spring的相关注解的类，则把这些类注册为Spring的bean -->
    <context:component-scan
        base-package="org.fkit.controller" />
    <!-- 静态资源处理(因为用到js,css文件) -->
    <mvc:default-servlet-handler />
    <!-- 设置配置方案 -->
    <mvc:annotation-driven>
        <!-- 设置不使用默认的消息转换器 -->
        <mvc:message-converters
            register-defaults="false">
            <!-- 配置Spring的转换器 -->
            <bean
                class="org.springframework.http.converter.StringHttpMessageConverter" />
            <bean
                class="org.springframework.http.converter.xml.SourceHttpMessageConverter" />
            <bean
                class="org.springframework.http.converter.ByteArrayHttpMessageConverter" />
            <bean
                class="org.springframework.http.converter.BufferedImageHttpMessageConverter" />
            <!-- 配置fastjson中实现HttpMessageConverter接口的转换器 -->
            <bean id="fastJsonHttpMessageConverter"
                class="com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter">
                <!-- 加入支持的媒体类型：返回contentType -->
                <property name="supportedMediaTypes">
                    <list>
                        <!-- 这里顺序不能反，一定先写text/html,不然ie下会出现下载提示 -->
                        <value>text/html;charset=UTF-8</value>
                        <value>application/json;charset=UTF-8</value>
                    </list>
                </property>
            </bean>
        </mvc:message-converters>
    </mvc:annotation-driven>

    <!-- 视图解析器 p:prefix属性表示前缀 p:suffix 表示后缀 -->
    <bean id="viewResolver"
        class="org.springframework.web.servlet.view.InternalResourceViewResolver"
        p:prefix="/WEB-INF/content/" p:suffix=".jsp" />

</beans>
```
