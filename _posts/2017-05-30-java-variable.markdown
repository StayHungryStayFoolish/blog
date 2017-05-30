---
layout:     post
title:      "Java 数据类型、变量"
subtitle:   ""
author:     "Bonismo"
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 基本数值类型
    - 布尔类型
    - 引用数据类型
---

## Java 数据类型

#### 基本数据类型

   - 布尔类型

        - boolean 分别为

                true / false 代表 真 / 假

   - 基本数值类型

        - 定点类型

            * 字节 byte

            * 字符 char 只占一个字符，包括中文

            * 短整型 short

            * 整型 int

            * 长整型 long 末尾要加 L ,不加默认为 int 类型

        - 浮点类型 [精度有损失]

            * 单精度浮点数 float  末尾要加 f ,不加默认为 dounle 类型

            * 双精度浮点数 double

#### 引用数据类型

   - 类 class

   - 接口 interface

   - 枚举 enum

   - 数组 array

## 基本数据类型的装箱

|基本类型|默认值|装箱类型|默认值|类型定义|取值范围|备注|
|---|:---:|:---:|:---:|:---:|:---:|:---:|
|boolean|false|Boolean|null|布尔值，作二元判断|true、false|
|byte|0|Byte|null|8位有符号整数，1字节|-128 ~ 127||
|char|0|Character|null|16位Unicode字符，2字节|0-65535|名称不同，char必须使用(int)强转|
|short|(short) 0|Short|null|16位有符号整数，2字节|-32768 ~ 32767||
|int|0|Integer|null|32位有符号整数，4字节|-2147483648 ~ 2147483647 |名称不同|
|long|(long) 0|Long|null|64位有符号整数，8字节|-2的63次方 ~ 2的63次方 -1)||
|float|0.0|Float|null|32位有符号整数，4字节|1.4E-45~3.4028235E38||
|double|0.0|Double|null|64位有符号整数，8字节|4.9E-324~1.7976931348623157E308||


###

封装类型可以输出，基本数据类型程序会报错，无 MAX_VALUE 属性

``` java

    public class Forever {
        public static void main(String[] args) {
            for (Integer i = 0; i < Integer.MAX_VALUE; i++){
                System.out.println("I Love My Girl");
            }
        }
    }

```

布尔类型运算

``` java

    boolean a = true;
    boolean b = true;
    System.out.println( a & b);
    逻辑与 &,同为 true，结果为 true 其余情况均为 false
    boolean a = true;
    boolean b = false;
    System.out.println( a | b);
    逻辑或 |有一个为 true，则为 true
    boolean a = true;
    boolean b = true;
    System.out.println( a ^ b);
    逻辑异或 ^同为一个值时，结果是false，不相同才为 true

    boolean a = true;
    System.out.println( !a );
    逻辑非 ！单目运算符，取反值

    条件与 && ，条件或 || 和逻辑与，或运算一样，但第一个运算能确定结果时，第二个不再计算，即短路。
    短路例子：
    int x = 2;
    int y = 1;
    boolean z = ( x < y ) && ( y++ < x )
    System.out.println( y );
    System.out.println( z );
    结果：y++ 没有计算，被短路
    y: 1
    z: false

    int x = 2;
    int y = 1;
    boolean z = ( x < y ) & ( y++ < x )
    System.out.println( y );
    System.out.println( z );
    结果：y++ 有计算
    y: 2
    z: false

    以上省去类结构

    变量定义在类中

    主方法：
    public static void main(String[] args){
        // 这里写输出语句
        System.out.println( 要输出的变量名字 );
    }

```