---
title: 示例 自定义HttpMessageConverter 接收JSON格式的数据
categories: 
  - 4 Spring+Mybatis企业应用实战(第2版)
  - 第3章 Spring MVC的常用注解
  - 3.13 @RequestBody注解
abbrlink: 6ba634ae
date: 2019-08-20 20:47:02
updated: 2022-04-03 01:21:16
---
# 示例 自定义HttpMessageConverter 接收JSON格式的数据
`Spring`默认使用`Jackson`处理`JSON`数据。在实际开发中,开发者也可以选择使用其他开源框架处理`JSON`数据。那么,如果使用其他的开源框架处理`JSON`数据,该如何配置`HttpMessageConverter`呢?接下来,我们就使用在业界非常受欢迎的`Fastjson`来接收`JSON`数据。
## 下载Fastjson
本书成书时`Fastjson`开源框架的最新版本是1.2.9。`jar`包只有1个:`fastjson-1.2.9.jar`。建议读者[进入该地址](http://mvnrepository.com/artifact/com.alibaba/fastjson)下载该版本或者更高版本进行测试。
# 项目示例
创建一个`FastjsonTest`项目,在`WebContent`目录下创建一个`js`目录,加入`jQuery`和`json2`的`js`文件,在`WEB-INF/lib`目录中加入`Fastjson`的`jar`文件。
## 项目结构
<details><summary>展开/折叠</summary><pre>
G:\Desktop\随书源码\Spring+Mybatis企业应用实战(第2版)\codes\03\FastjsonTest
├─src\
│ └─org\
│   └─fkit\
│     ├─controller\
│     │ └─<a href="#BookController-java">BookController.java</a>
│     └─domain\
│       └─Book.java
└─WebContent\
  ├─index.jsp
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
    ├─<a href="#springmvc-config-xml">springmvc-config.xml</a>
    └─web.xml

</pre></details>

## BookController.java
```java
package org.fkit.controller;

import javax.servlet.http.HttpServletResponse;
import org.fkit.domain.Book;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import com.alibaba.fastjson.JSONObject;

@Controller
@RequestMapping("/json")
public class BookController
{
    // @RequestBody可以将json数据转换成对应的Object
    @RequestMapping(value = "/testRequestBody")
    public void setJson(@RequestBody Book book, HttpServletResponse response)
            throws Exception
    {
        // JSONObject-lib包是一个beans,collections,maps,java arrays和xml和JSON互相转换的包。
        // 使用JSONObject将book对象转换成json输出
        System.out.println(JSONObject.toJSONString(book));
        book.setAuthor("作者名字");
        response.setContentType("text/html;charset=UTF-8");
        // 将book对象转换成json写出到客户端
        response.getWriter().println(JSONObject.toJSONString(book));
    }
}
```
## springmvc-config.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:p="http://www.springframework.org/schema/p"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:util="http://www.springframework.org/schema/util"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd     
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/util
        http://www.springframework.org/schema/util/spring-util.xsd">

    <!-- spring可以自动去扫描base-pack下面的包或者子包下面的java文件，-->
    <!-- 如果扫描到有Spring的相关注解的类，则把这些类注册为Spring的bean -->
    <context:component-scan
        base-package="org.fkit.controller" />
    <!-- 静态资源处理 -->
    <mvc:default-servlet-handler />

    <!-- 设置配置方案 -->
    <mvc:annotation-driven>
        <!-- 设置不使用默认的消息转换器 -->
        <mvc:message-converters register-defaults="false">
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
以上配置文件和之前的配置文件主要的区别在于:
- 之前使用的是`Spring`中默认的`MappingJackson2HttpMessageConverter`,这样只需要配置默认的`<mvc:annotation-driven/>`就可以了。
- 而现在使用第三方的开源框架`Fastjson`处理`JSON`数据,则需要另行配置`HttpMessageConverter`。

`Spring MVC`默认使用`MappingJackson2JsonView`转换器,所以必须加入`Jackson`这个库的第三方类文件。而在实际开发中,更加受欢迎的是`Fastjson`,所以本例并没有使用`Jackson`,而是使用了`Fastjson`,则转换器需要配置成`com.alibaba.fastjson.support.spring.FastJsonHttpMessageConverter`类型,该类是`Fastjson`中实现了`HttpMessageConverter`接口的类。
如果加入了`Fastjson`相关`jar`文件,但是没有配置`FastJsonHttpMessageConverter`转换器,则在发送请求时后台会提示错误:
```
Handler execution resulted in exception: Content type application/json;charset=UTF-8 not supported
```
此外,其他`JSP`和`Java`文件和之前项目的一致,并且还需要在`web.xml`文件中配置`Spring MVC`的前端控制器`DispatcherServlet`,因为每次配置基本一致,此处不再赘述读者可自行配置.
## 测试
部署`FastjsonTest`这个`Web`应用,在浏览器中输入如下`URL`来测试应用:
```
http://localhost:8080/FastjsonTest/
```
浏览器显示效果:
```
编号：1
书名：书的名字
作者：作者名字
```
由此可知,**处理`JSON`格式的开源框架使用`Jackson`和`Fastjson`,只是需要使用不同的`HttpMessageConverter`而已**.
