---
layout:     post
title:      "Java 集合框架之 -- Iterator/ListIterator"
subtitle:   "迭代器"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-14
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Iterator
    - ListIterator
    - 迭代
---

### 迭代器

- Iterator 接口提供了对很多元素进行迭代的方法。

    - 只迭代 List、Set，不迭代 Map

- ListIterator 也是 `接口`

    - ListIterator 继承于 Iterator

- 迭代器可以在迭代过程，删除底层集合元素

- cloning、serialization 语义和含义都跟具体的实现相关，由具体实现来绝对如何被克隆、序列化


### 迭代器方法

- Iterator 方法

    - hashNext() 如果仍有元素，返回 true `经常放在 for、while 循环中，做判断使用`

    - next() 返回迭代的下一个元素 `有时使用在移动指针的情况`

    - remove() 在迭代底层删除返回的最后一个元素

- ListIterator 方法

    - add()

    - hansNext()

    - hasPrevious()

    - next()

    - `nextIndex()`

    - previous()

    - `previousIndex()`

    - remove()

    - `set(E e)`

### 区别

||Iterator|ListIterator|备注|
|---|:---:|:---:|:---:|
|遍历集合|List、Set|List||
|方向|向前遍历|向前遍历、向后遍历||
|索引|不能获取 `index`|可以在任何时刻获取`index`|ListIterator 可以使用 previousIndex、 nextIndex 方法|
|添加|遍历时不能添加元素|可以使用 add 方法|List 遍历添加元素会抛 ConcurrentModificationException 异常|
|替换|不能替换|可以使用 set 方法替换||
