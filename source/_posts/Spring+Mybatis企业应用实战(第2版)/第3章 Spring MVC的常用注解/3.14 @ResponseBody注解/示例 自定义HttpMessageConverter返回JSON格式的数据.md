---
title: 示例 自定义HttpMessageConverter返回JSON格式的数据
categories: 
  - Spring+Mybatis企业应用实战(第2版)
  - 第3章 Spring MVC的常用注解
  - 3.14 @ResponseBody注解
date: 2019-08-20 21:55:02
updated: 2019-11-02 10:12:05
abbrlink: 830b4262
---
<div id='my_toc'>

- [示例 自定义HttpMessageConverter返回JSON格式的数据](/JavaReadingNotes/830b4262/#示例-自定义HttpMessageConverter返回JSON格式的数据)

</div>
<!--more-->
<script>if (navigator.platform.toLowerCase() == 'win32'){document.getElementById('my_toc').style.display = 'none';}</script>

<!--end-->
<!--SSTStart-->
# 示例 自定义HttpMessageConverter返回JSON格式的数据 #
接下来,使用`Fastjson`来返回`JSON`数据。
创建一个`Fastjson2Test`项目,在`WebContent`目录下创建一个`js`目录,加入`jQuery`和`json2`的`js`文件,在`WEB-INF/lib`目录中加入`Fastjson`的`jar`文件。
`Fastjson2Test`项目的所有`JSP`和`Java`文件和`ResponseBodyTest`一致,只是在`springmvc-config.xml`中使用了`Fastjson`的`FastJsonHttpMessageConverter`。读者可参考配套资源文件中对应的代码,测试结果和`ResponseBodyTest`项目一致,此处不再赘述.
<!--SSTStop-->

