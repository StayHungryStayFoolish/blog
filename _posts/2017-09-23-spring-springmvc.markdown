---
layout:     post
title:      "Spring Framework --- SpringMVC"
subtitle:   "三大组件"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-28
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - SpringMVC
    - 前端控制器
    - 处理器映射器
    - 处理器适配器
    - 视图解析器
---

### SpringMVC 架构流程

<div>
    <img src="https://github.com/StayHungryStayFoolish/stayhungrystayfoolish.github.io/blob/master/img/java/springmvc.png?raw=true"  />
</div>

### 组件说明

- DispatcherServlet 前端控制器

   整个流程控制中心枢纽，负责调用其他组件处理用户请求。


