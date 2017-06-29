---
layout:     post
title:      "Java 数据类型、变量"
subtitle:   "基础知识"
author:     "Bonismo"
date:       2017-05-30
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

- 算术运算符

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

- 其他运算符

    - cast 类型强转(强转有风险)

    - 合法类型转换

        - ——> 无损失

        - -`-> 可能有精度损失

        - ——> 或 -`-> 逆向需要强转

                 char ——> int

                 byte ——> short ——> int ——> long

                 int ——> double

                 int --> float

                 long --> float

                 long --> double

### Java 运算优先级

- 非 > 算术 > 关系 > 与 > 或 > 赋值

### Java 程序运行结构

- 顺序结构

- 选择结构(boolean 类型)

    - if 当 true 会执行

    - if () else (if) {} 注意 else 有无区别 if 不为 true 进入 else 执行

    - switch / case 条件选择 Since JDK1.7 支持 String(字符串类型)

- 循环结构

    - for 普通循环

    - for-each 增强循环

    - while

    - do / while

    - 循环结构控制关键词:

        - break 跳出当前循环，入嵌套循环，执行外层

        - continue 跳出本次循环，继续执行

        - return 退出循环


### 例：

- if 语句

        if ( 布尔表达式 ) {
            //如果布尔表达式为true将执行的语句
        }

        如果布尔表达式的值为 true，则执行 if 语句中的代码块，否则执行 if 语句块后面的代码

        public class Test {
            public static void main(String args[]){
                int x = 10;
                if( x < 20 ){
             System.out.print("这是 if 语句");
              }
           }
        }

- if...else语句

        if ( 布尔表达式 ){
           //如果布尔表达式的值为true
        }else{
           //如果布尔表达式的值为false
        }

        public class Test{
            public static void main(String args[]){
                int x = 30;
                if(x < 20){
                   System.out.print("这是 if 语句”);
                }else{
                   System.out.print("这是 else 语句”);
                }
            }
        }

- if...else if...else 语句

    - if 语句后面可以跟 else if… else 语句，这种语句可以检测到多种可能的情况。

        使用 if，else if，else 语句的时候，需要注意下面几点：

        if 语句至多有 1 个 else 语句，else 语句在所有的 else if 语句之后。

        if 语句可以有若干个 else if 语句，它们必须在 else 语句之前。

        一旦其中一个 else if 语句检测为 true，其他的 else if 以及 else 语句都将跳过执行。

- if...else 语句语法:

        if(布尔表达式 1){
             //如果布尔表达式 1的值为true执行代码
             }else if(布尔表达式 2){
            //如果布尔表达式 2的值为true执行代码
             }else if(布尔表达式 3){
            //如果布尔表达式 3的值为true执行代码
             }else{
            //如果以上布尔表达式都不为true执行代码}

        public class Test{
            public static void main(String args[]){
                int x = 30;
                if(x == 10){
                    System.out.print("Value of X is 10”);
                }else if(x==20){
                    System.out.print("Value of X is 20”);
                }else if(x==30){
                    System.out.print("Value of X is 30”);
                }else{
                    System.out.print("这是 else 语句”);
                }
            }
        }

- 嵌套的 if…else 语句

        使用嵌套的 if…else 语句是合法的。也就是说你可以在另一个 if 或者
         else if 语句中使用 if 或者 else if 语句【需要深度理解】。

        嵌套的 if…else 语句语法：
        if(布尔表达式1){
          // 如果布尔表达式 1 的值为 true 执行代码
             if(布尔表达式2){
          // 如果布尔表达式 2 的值为 true 执行代码
             }
        }

- switch 语句

        switch 语句语法：

        switch(expression){
              case value:
              //语句
              break;
         //可选case value:
              //语句
              break;//可选
              //你可以有任意数量的case语句
              default://可选
              //语句
        }

- switch 语句有如下规则：

 switch 语句中的变量类型可以是： byte、short、int 或者 char。
 **从 Java SE 7 开始，switch 支持 String（字符串类型）了，**
 **同时 case 标签必须为字符串常量或字面量。**
 switch 语句可以拥有多个 case 语句。每个 case 后面跟一个要比较的值和冒号。
 case 语句中的值的数据类型必须与变量的数据类型相同，而且只能是常量或者字面常量。
 当变量的值与 case 语句的值相等时，那么 case 语句之后的语句开始执行，
 直到 break 语句出现才会跳出 switch 语句。
 当遇到 break 语句时，switch 语句终止。程序跳转到 switch 语句后面的语句执行。
 case 语句不必须要包含 break 语句。如果没有 break 语句出现，
 程序会继续执行下一条 case 语句，直到出现 break 语句。
 switch 语句可以包含一个 default 分支，该分支必须是 switch 语句的最后一个分支。
 default 在没有 case 语句的值和变量值相等的时候执行。
 **default 分支不需要 break 语句。**

- 例

            public class Test{
                public static void main(String args[]){
                    //char grade = args[0].charAt(0);
                    char grade='C’;
                    switch(grade){
                        case'A’:
                            System.out.println("优秀”);
                        break;
                        case'B’:
                        case'C’:
                            System.out.println("良好”);
                        break;
                        case'D’:
                            System.out.println("及格”);
                        case'F’:
                            System.out.println("你需要再努力努力”);
                        break;
                        default:
                            System.out.println("未知等级”);
                     }
                    System.out.println("你的等级是"+grade);
                }
            }

- 注意 case 后边的是冒号，执行case 条件句，遇到正确的，break 跳出当前循环，执行 defult 后边语句