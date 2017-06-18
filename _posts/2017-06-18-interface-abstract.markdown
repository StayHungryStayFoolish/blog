---
layout:     post
title:      "Java 接口比抽象更抽象"
subtitle:   ""
iframe:     ""
navcolor:   "invert"
date:       2017-05-30
author:     "Bonismo"
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 接口
    - 抽象类
    - 设计层次
    - 使用场景
---

## 接口

- 接口是一种比抽象类更加抽象的 "类”。

- 接口不是类，是跟类同级别的一种存在。

- 接口中，只存在 常量 `static final` ，抽象方法`abstract`。

- 接口时对外提供服务的。

## 设计层次

- 抽象层次不同：

    - 接口是对行为抽象。

    - 抽象类是对类抽象。

- 跨域不同：

    - 接口跨域不同的类。

        - 实现接口的类之间可以不存在任何关系，共同之处，类似一种契约。例如：接口定义 fly(); 抽象方法，Animal 类的动物鸟，可以实现接口。Vehicle 类的飞机，可以实现接口。


        - 抽象类必须被子类实现，抽象类所体现的是一种继承关系，体现子父类之间的自上而下的关系。

    - 抽象类所跨域的是具有相似特点的类。Animal 类的鸟、狗都会叫，这个就是抽象方法。都可以吃东西，这个就是抽象方法。然后抽象出来一个 Animal 抽象类。


