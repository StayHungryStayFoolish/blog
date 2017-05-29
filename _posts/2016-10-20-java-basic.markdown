---
layout:     post
title:      "语言基础"
subtitle:   ""
iframe:     ""
navcolor:   "invert"
date:       2016-10-20
author:     "Bonismo"
tags:
    - 标识符
    - 命名规范
    - 关键字
---

## 标识符

用来起名的字符，有些字符是不可以随便用的。就像古人讲的避讳。

- 首字符不能是数字

- 字母/数字/下划线/美元符号 $ 可以作为起始字符

- 区分大小写

- 不能是关键字以及 true / false (true / false 就像潘多拉魔盒)

## 命名规范

### 编程最头疼的事，不是空指针，不是设计思想，而是命名

<div>
    <img src="https://github.com/StayHungryStayFoolish/stayhungrystayfoolish.github.io/blob/master/img/java/name.jpg?raw=true" height="700" width="600" />
</div>


该结果是来自Quora(等同于国内的知乎)问答网站和更早的Ubuntu论坛跟帖的4500个开发者的投票。

如何命名一项的选票几乎是其它八项的投票结果的总和。

通常，如果你无法想出一个合适的名字，意味着你的设计可能有问题。

让然可以使用下边链接。

[http://unbug.github.io/codelf/]

支持直接搜索中文，当你查中文的时候，Codelf 会直接查好单词和单词的近义词给你，

然后再搜索Github, Bitbucket, Google Code, Codeplex, Sourceforge, Fedora Project上的

开源项目的源码匹配出与这些词汇相关的变量名和函数名。Codelf 可以选择开发语言进行搜索，

结果会把同个源码文件里匹配的变量名排在一起,如你选择“Java”然后搜索“苹果”

- Camel Case 驼峰命名

    - 首个单词字母大写，第二个单词首字母大写 HelloWorld

    - 避免使用拼音、禁止使用汉字


- 命名要点

    - List 定义的变量 应该 List 后缀结尾 arrayList

    - Map 定义的变量 应该 Map 后缀结尾 hashMap

    - Array 数组定义的变量 应该 s 后缀结尾 students

    - 尽量避免过长命名

    - 方法名尽量命名为该方法实现的功能 getName




