---
layout:     post
title:      "Java 语言基础"
subtitle:   ""
iframe:     ""
navcolor:   "invert"
date:       2016-10-20
author:     "Bonismo"
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
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

<p>「 Codelf 变量命名  」<a href="http://unbug.github.io/codelf/" target="_blank">「 Codelf 变量命名 」</a></p>

支持直接搜索中文，当你查中文的时候，Codelf 会直接查好单词和单词的近义词给你，

然后再搜索Github, Bitbucket, Google Code, Codeplex, Sourceforge, Fedora Project上的

开源项目的源码匹配出与这些词汇相关的变量名和函数名。Codelf 可以选择开发语言进行搜索，

结果会把同个源码文件里匹配的变量名排在一起,如你选择“Java”然后搜索“苹果”

#### 类名

- Camel Case 驼峰命名

    - 首个单词字母大写，第二个单词首字母大写 HelloWorld

    - 避免使用拼音、禁止使用汉字

#### 方法及变量名字


- 命名要点 首字母小写，第二个以后每个单词首字母大写

    - List 定义的变量 应该 List 后缀结尾 arrayList

    - Map 定义的变量 应该 Map 后缀结尾 hashMap

    - Array 数组定义的变量 应该 s 后缀结尾 students

    - 尽量避免过长命名

    - 方法名尽量命名为该方法实现的功能 getName

#### 关键字

|类别|关键字|说明|
|---|:---:|:---:|
|访问控制|||
||private|私有的|
||protected|受保护的|
||public|公共的|
|-|-|-|
|类、方法和变量修饰符|||
||abstract|声明抽象|
||class|类|
||extends|继承、扩展|
||final|终极、不可改变|
||implements|实现|
||interface|接口|
||native|本地|
||new|新建、创建|
||static|静态|
||strictfp|精准|
||synchronized|同步|
||transient|短暂|
||volatile|不稳定|
|-|-|-|
|控制语句|||
||break|跳出当前循环|
||continue|继续|
||return|返回|
||do|运行|
||while|循环|
||if|如果|
||else|否则|
||for|循环|
||instanceof|实例|
||switch|选择执行|
||case|条件，switch 来选择|
||default|默认|
|-|-|-|
|错误处理|assert|断言表达是否为真|
||catch|捕获异常|
||finally|有无异常均执行|
||throw|抛出异常对象|
||try|视图捕获异常|
|和包相关的|||
||import|导入|
||package|包|
|基本类型|||
||boolean|布尔类型  true/false两种类型|
||byte|字节型|
||char|字符型|
||double|双精度浮点|
||float|单精度浮点|
||int|整型数值|
||long|长整型|
||short|短整型|
||null|空，不存在|
|变量引用|||
||super|父类、超类|
||this|本类|
||void|无返回值的方法|
|保留关键字|goto|不是关键字，但不能使用，历史遗留|
|后续补充|||

以上内容前期了解，中期必须掌握。

