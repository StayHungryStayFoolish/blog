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

### ArrayList、LinkedList

||AarrayList|LinkedList|备注|
|---|:---:|:---:|:---:|
|结构|数组形式|链表形式||
|索引|有`index`|无||
|访问|根据索引随机访问|支持首尾||
|插入、删除|慢|快|ArrayList需要移动，LinkedList 只需改变前后指针指向|
