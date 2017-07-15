---
layout:     post
title:      "Java 集合框架之 -- Set"
subtitle:   "Set 集合"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-14
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - HashSet
    - LinkedHashSet
    - TreeSet
---

## Set 集合

- Set 是一个`接口`，继承于 Collection

- 无序

- 不允许重复元素，只允许有一个 Null 存在。

## Set 主要实现类

- HashSet `无序`

    - LinkedHast 继承于 HashSet 以 `元素插入顺序排序`

- TreeSet 按元素`自然顺序排序`，因为实现了 NavigableSet 接口


### HashSet 特性

- 使用 HashMap 来存储元素，因为 HashSet 是 HashMap 的一个实例。

- 无序

- 效率高

- 不同步，多线程不安全

- 初始容量16，加载因子是0.75

- 构造器支持设置初始容量

- 不支持快速随机遍历，只能通过迭代器进行遍历 iterator 。

### LinkedHashSet 特性

- 支持以元素插入顺序进行维护的`链表`

- 允许以`插入`的顺序在集合器中迭代

- 按元素`插入`顺序进行排序

- 初始容量16，加载因子是0.75

- 不同步，多线程不安全

- 构造器支持设置初始容量

- 不支持快速随机遍历，只能通过迭代器进行遍历 iterator 。

### TreeSet

- 实现 NavigableSet，所以支持元素的`自然顺序`排序

- 不支持快速随机遍历，只能通过迭代器进行遍历 iterator 。

- 不同步，多线程不安全

