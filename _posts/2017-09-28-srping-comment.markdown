---
layout:     post
title:      "Spring Framework --- Comment"
subtitle:   "注解详解"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-28
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - @Controller
    - @Service
    - @Repository
---

### SpringMVC 常用注解

- @Controller

    在 Spring MVC 中，控制器 Controller 负责处理由 `DispatcherServlet` 分发的请求，它把用户请求的数据经过业务处理层处理之后封装成一个 Model，然后再把该 Model 返回给对应的 View 进行展示。

