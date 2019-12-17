---
title: 第3章 Spring MVC的常用注解
categories: 
  - Spring+Mybatis企业应用实战(第2版)
  - 第3章 Spring MVC的常用注解
  - 3.0 本章要点
date: 2019-08-17 09:20:20
updated: 2019-12-17 01:45:46
abbrlink: 7ae44303
---
<div id='my_toc'><a href="/JavaReadingNotes/7ae44303/#第3章-Spring-MVC的常用注解" class="header_1">第3章 Spring MVC的常用注解</a><br><a href="/JavaReadingNotes/7ae44303/#本章要点" class="header_2">本章要点</a><br></div>
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
# 第3章 Spring MVC的常用注解 #
## 本章要点 ##
- `@Controller`注解
- `@RequestMapping`注解
- `@GetMapping`注解
- `@PostMapping`注解
- `@RequestParam`注解
- `@PathVariable`注解
- `@MatrixVariable`注解
- `@CrossOrigin`注解
- `@RequestHeader`注解
- `@CookieValue`注解
- `@RequestAttribute`注解
- `@SessionAttribute`注解
- `@SessionAttributes`注解
- `@ModelAttribute`注解
- `@RequestBody`注解
- `@ResponseBody`注解
- `@RestController`注解
- `@ResponseStatus`注解
- `@ExceptionHandle`注解
- `@ControllerAdvice`注解
- `@RestControllerAdvice`注解

`Spring`从2.5版开始引入注解,用户可以在`Spring MVC`中使用`@Controller`、`@RequestMapping`、`@RequestParam`、`@ModelAttribute`等类似的注解。到目前为止, `Spring`的版本虽然发生了很大的变化,但注解的特性却一直延续下来,并不断扩展,让广大开发者的工作变得更轻松。这都离不开注解的强大作用,本章将重点讲解`Spring MVC`中常用的注解
<!--SSTStop-->

