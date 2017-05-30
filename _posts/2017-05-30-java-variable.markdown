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


### 装箱和不装箱的区别

- 自动装箱 AutoBoxing JDK1.5

- 自动拆卸 Auto-UnBoxing JDK1.5

- 基本类型和封装类型混合使用时，会自动拆箱。

1.基本类型只有值；装箱后有值和不同的引用

2.基本类型只有一个功能值（表示大小）；装箱后有功能值和非功能值（可以表示 null ）

3.基本类型比装箱后的节省时间和空间

### 例：

封装类型可以输出，基本数据类型程序会报错，无 MAX_VALUE 属性

``` java

    public class Forever {
        public static void main(String[] args) {
            for (Integer i = 0; i < Integer.MAX_VALUE; i++){
                System.out.println("I Love My Girl");
            }
        }
    }
    // 不建议低配置运行
```

浮点精度损失问题

```java

    System.out.pritln( 1d - 0.9d );
    System.out.pritln( 1f - 0.9f );
    System.out.pritln( 1 - .9 );

    输入结果都是：0.099999999998

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

### 运算符

- 算数运算符

        +  运算顺序是从左至右，其他类型与字符串的 + 为字符串拼接

        -

        *

        / 整数除法，截去余数，不四舍五入

        % 模运算，求余数，符号至于被除数有关

- 关系运算符

        >

        <

        >=

        <=

        == 任意类型比较

        != 任意类型比较

- 布尔逻辑运算符

        & 逻辑    与

        | 逻辑    或

        ^        异或

        !        非

        && 条件   与

        || 条件   或

        短路规则： &&  ||

        第一个表达式即可确定运算结果时，不再判断第二个表达式

        使用短路规则与否，可能副作用不同

- 赋值类运算符

        =

        +=

        -=

        *=

        /=

        %=

        &= 针对布尔或定点类型

        |= 针对布尔或定点类型

- 位运算符

    不做补充

- 条件运算符

    (condition)?(true_value):(false_value) 三目运算符  掌握

        三目运算法则：

        表达式1 ？表达式2 : 表达式3

        表达式1的类型必须是 boolean 类型(或者是可以通过拆箱转换为boolean类型的Boolean类型)，

        当表达式1的值为 true 时，条件表达式的结果就是表达式2的值，

        当表达式1的值为 false 时，结果为表达式3的值。表达式2与表达式3的类型可以是任意类型。
