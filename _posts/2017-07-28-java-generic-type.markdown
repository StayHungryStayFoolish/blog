---
layout:     post
title:      "Java Generic Types"
subtitle:   "泛型简介"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-06-29
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 泛型
    - 类型安全
    - 类型检查
    - 简化代码
---

### Generic Types 泛型

- Since Java JDK 5

- 泛型，即泛化的类型

开篇之初，曾提到过基本数据类型、引用数据类型还有基本数据类型的自动拆箱和装箱。
其中提到过强转，包括精度损失问题。

仔细查看 API 文档会发现，Java 一切类的向上类最终都能追溯到一个父类，即`Object`类。
也就是说，所有的类都可以向上转为 Object 类。

但是如果不是向上转，而是不同类型之间转换呢？

所以 Java 自 JDK 5 以后引入了`Generic Types` 泛型的概念。

