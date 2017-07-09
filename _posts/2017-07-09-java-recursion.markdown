---
layout:     post
title:      "Java 递归调用示例"
subtitle:   "递归"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-09
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 递归
---

## 递归

- 函数自身调用自身

### 递归场景

- 当一个功能被重复使用，而每一次使用该功能的参数不确定，都由上次的功能元素结果来确定。

- 简单说：功能内部又用到该功能，但是传递的参数值不确定。( 每次功能参与运算的值不确定 )

### 注意事项

- 一定要定义递归条件

- 递归次数不要过多，不然容易出现堆栈内存溢出错误。

### 递归技巧

- 掌握好递归算法的出口。这个是最重要的。

    - 即：i == n 条件

### 将一个正整数分解为质因数

- 例：




