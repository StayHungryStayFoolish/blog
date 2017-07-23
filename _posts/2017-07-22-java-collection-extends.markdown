---
layout:     post
title:      "Java 集合框架之 -- 扩展"
subtitle:   "各种异同"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-14
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 容量
    - 结构
    - 排序
---


### Collection、Map

<div>
    <img src="https://github.com/StayHungryStayFoolish/stayhungrystayfoolish.github.io/blob/master/img/java/collection.jpg?raw=true" />
</div>


||Collection|Map|备注|
|---|:---:|:---:|:---:|
|结构|每个位置只存一个元素，允许 null 存在|Key-Value结构，Key不允许 null|Map 像小型数据库|
|形式|元素的集合|元素映射||

### List、Set

||List|Set|备注|
|---|:---:|:---:|:---:|
|结构|列表|集合||
|元素|元素可以重复，多个 null|不可以重复，只允许一个 null||

### ArrayList、LinkedList

||AarrayList|LinkedList|备注|
|---|:---:|:---:|:---:|
|结构|数组形式|链表形式||
|索引|有`index`|无||
|顺序|有序|无序||
|访问|`快`根据索引随机访问|`慢`支持首尾||
|插入、删除|慢|快|ArrayList需要移动，LinkedList 只需改变前后指针指向|
|场景|快速随机访问|频繁操作数据||

### HashSet、LinkedHashSet、TreeSet
||HashSet|LinkedHashSet|TreeSet|备注|
|---|:---:|:---:|:---:|:---:|
|容量|16|16|无||
|次序|无序|插入顺序|自然顺序|TreeSet 实现 NavigableSet接口|

### 容量、同步

|实现类|初始容量|扩容|capacity|同步|备注|
|---|:---:|:---:|:---:|:---:|:---:|
|ArrayList|10|1.5倍|无|NO|原容量取0.5有奇数时，选较小值|
|LinkedList|※|API无说明|无|NO|
|Vector|10|2倍|`有`|`YES`|||
|HashSet|16|0.75|无|NO||
|HashTable|11|0.75|无|YES||
|LinkedHashSet|16|0.75|无|NO||
|TreeSet|※|※|无|NO|红-黑树结构|
|HashMap|16|0.75|无|NO||
|LinkedHashMap|16|0.75|无|NO||
|TreeMap|※|※|无|NO|红-黑树结构|