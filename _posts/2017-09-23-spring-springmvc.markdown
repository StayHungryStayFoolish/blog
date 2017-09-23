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

   降低了组件之间的耦合度。

- HandlerMapping 处理器映射器

    负责找到 Handler(处理器)。

- HandlerAdapter 处理器适配器

    对处理器进行执行

- ViewResolver 视图解析器

   负责将处理结果生成 View 视图，视图解析器会根据逻辑视图解析成物理视图（具体 URL 页面）
   再生成 View 视图对象，最后进行渲染将处理结果通过页面展示给用户。


### XML 文件



- 在 spring-mvc.xml 中

    配置 处理器映射器、处理器适配器

        `<mvc:annotation-driven>`

    配置组件扫描器，可以批量扫描 @Controller @Service

        `<context:component-scan>`

    视图解析器

        <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
            <property name="viewClass" value="org.springframework.web.servlet.view.JstlView"/>
            <property name="prefix" value="/WEB-INF/jsp/"/>
            <property name="suffix" value=".jsp"/>
        </bean>
