---
layout:     post
title:      "Spring Framework --- Spring"
subtitle:   "控制反转、面向切面"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-28
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Spring
    - IOC
    - AOP
---

### Spring 框架

- Spring 框架是一个为 Java 应用程序开发提供了综合、广泛的基础性支持的 Java 平台。

- Spring 帮助开发者解决了开发者的基础性问题，使开发更专注于应用程序的开发，解决实际需求。

### Spring 模块结构

<div>
    <img src="https://github.com/StayHungryStayFoolish/stayhungrystayfoolish.github.io/blob/master/img/java/spring.png?raw=true" />
</div>


### Spring 框架核心组件

- Core

- Context

- Beans

### Beans

`核心组件内，最核心的是 Beans，最核心功能是 Bean Factory`

Bean 组件在 org.springframework.beans 包下。

- Bean 的定义

- Bean 的创建

- Bean 的解析

### Spring三大核心思想

- DI （依赖注入）

- IOC (控制反转)

- AOP（面向切面）

### DI 依赖注入

- 某个类需要依赖其他类的方法来做事情时，通常需要 new 一个依赖类，再调用该实例的方法。
  就像上篇文章介绍的一样，而这种开发存在很多问题，所以 Spring 提出了`依赖注入`的思想，
  即依赖类的实例化交给 Spring 容器来做，开发过程中，只需要创建 Bean 即可，
  Spring 会完成对 Bean 的定义与解析。

- 依赖注入的作为是通过 JavaBean 属性或构造方法传递给需要的对象。

    - 属性注入，即设值注入（Setter Injection）,类似上文中的 set 方法。

    - 构造器注入，即构造子注入（Constructor Injection）,类似上文中的构造器方法。

    `但框架中的会更复杂些，原理是一样的`

### IOC 控制反转

- 控制反转和依赖注入差不多。

- 区别在于：

    - 依赖注入，组件不做`定位查询`。只提供普通的 Java 方法让容器去决定依赖关系。
      容器负责组件装配，将符合依赖关系的对象传递过去。`更侧重于实现`

    - 控制反转，组件会做`定位查找`。创建对象实例的控制器从代码控制被剥离到了 IOC 容器控制。`更侧重于原理`

- 通俗理解就是

   - `控制反转，调用者不在创建被调用实例。`

   - `依赖注入，容器创建好实例，再注入调用者。`


### IOC 和 DI 都说明了 Spring 采用动态、灵活的方式来管理各种对象。

### AOP 面向切面

- 动态的将代码切入到类的指定方法、指定位置上。

- `通俗理解：嫁接`

    - 你要在一颗苹果树上，结出西瓜大的苹果。就需要在苹果树上，切开一个口，
      把西瓜的东西包进去，然后再合上，于是西瓜大的苹果就有了。


### Spring 、 SpringMVC

- Spring 是一个管理 Bean 的容器，也是很多开源项目的总称。

- SpringMVC 是 Spring 其中一个开源项目

- 在 Spring - SpringMVC - MyBatis 框架中，大致`工作流程`

  1. 一个 Http 请求，由应用程序容器（Tomcat）解析，转换为一个 request，

  2. 通过 @Controller 注解，进入 SpringMVC 容器

  3. SpringMVC 容器的前端控制器 DispatcherServlet 会去处理这个请求 Bean

  4. Bean Factory 创建 Bean，然后依次进入 @Service @Dao 层 最后通过视图渲染传回到页面