---
layout:     post
title:      "Java 静态、构造器、非静态之初始化顺序"
subtitle:   "有序输出"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-06-29
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 静态域
    - 静态块
    - 非静态块
    - 构造函数
---

## 块 概念

- 无名

- 无参数

- 无返回类型

- `静态块` 有 static 修饰

        {
            // 方法体
        }


        static{
            // 方法体
        }


