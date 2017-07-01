---
layout:     post
title:      "Java 数组 - 基础"
subtitle:   "Basic Array"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-06-29
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 数组概念
    - 声明、初始化、创建
    - 特性
---

## 数组

- 同一类型值的集合

- 数组是静态的

- 数组的声明、初始化、创建是一个整体过程

- 数组具有索引（下标）index

- 数组是有长度的，length，推荐循环时，使用 length，不会出现下标越界

- 数组需要遍历

    - 循环来输出 for for-each 循环

- 一维数组、二维数组、多维数组

### 数组的定义方式

- 动态定义 String[ ] aArray = new String`[` 5 `]`;

- 静态定义 String[ ] bArray = {"a","b","c","d","e"}

- 静态定义 String[ ] cArray = new String[ ]{"a","b","c”,"d","e”}


        第一种定义了一个数组，并指定了数组的长度，属于动态定义。

        第二种和第三种在分配内存空间的同时，还初始化了值。

- 数组声明，创建，初始化必须都放在一条语句中，分开会出现语法错误。

- 典型错误：

int[ ] ints;

ints = {1,2,3,4,5};
语句分开，直接报错。

- 特殊情况

    二维、多维数组，只定义 行 就可以，不会报错。

    int[ ][ ] a = new int`[`3`]`[ ];
    System.but.println(a.length); // 3

    int[ ][ ] b = new int`[`3`]` `[`5`]`;
    System.out.println(b.length); // 3

    int[ ] arr = new int`[` 3 `]`;
    System.out.println(arr.getClass());

### 打印数组

- Arrays.toString(arr);

- Arrays.deepToString(arr);

    deepToString(); 更适合打印多维数组

        String[][] b = new String[3][4];
              for (int i = 0; i < 3; i++){
                  for (int j = 0; j < 4; j++){
                      b[i][j] = "A" + j;
                      }
                  }
                  System.out.println(Arrays.toString(b));
                  //输出[[Ljava.lang.String;@55e6cb2a, [Ljava.lang.String;@23245e75, [Ljava.lang.String;@28b56559]

                  System.out.println(Arrays.deepToString(b));
                  //输出[[A0, A1, A2, A3], [A0, A1, A2, A3], [A0, A1, A2, A3]]


- 数组输出形式

        class Demo{
            public static void main(String[] args) {
                int[] intArray = {1, 2, 3, 4, 5, 6};
                String intArrayString = Arrays.toString(intArray);

                System.out.println(intArray); // 输出的是一个 String 类型的 Hex 码
                System.out.println(intArrayString); // 输出的是一个 String 类型
            }
        }

        结果：
        [I@511d50c0
        [1, 2, 3, 4, 5, 6]

### 通过反射机制访问数组元素

- 反射机制 是通过 java.lang.reflect.Array 这个类来处理数组。

    reflect /rɪ'flekt/ 反射、反映

- 可以使用 Array.get(); Array.set(); 方法访问数组，设置数组。

        public class ArrayReflect {
            public static void main(String[] args) {
                // 注意定义数组的方式  因为是反射机制，所以要定义 一个实例，实例的参数是一个关于 class 的数据类型。要有强转 (Parameter_Type)
                int[] intArray = (int[]) Array.newInstance(int.class, 3);
                Array.set(intArray, 0, 123);
                Array.set(intArray, 1, 456);
                Array.set(intArray, 2, 789);
                System.out.println("intArray[0] = " + Array.get(intArray, 0));
                System.out.println("intArray[1] = " + Array.get(intArray, 1));
                System.out.println("intArray[2] = " + Array.get(intArray, 2));    }
        }

        输出：
        intArray[0] = 123
        intArray[1] = 456
        intArray[2] = 789

### 数组简单方法实例

- 检测是否包含某一个元素

    boolean b = Arrays.asList(数组名字).contains(元素);

- 复制一个数组的元素，从数组起始位置复制

    数组类型[ ] 数组名字2 = Arrays.copyOf(数组名字1, 复制的长度);

- 复制一个数组的元素，从指定位置复制

    数组类型[ ] 数组名字2 = Arrays

    .copyOfRange(数组名字1, 指定位置，结束位置);

        public class ArrayDemmo{
            // 数组类型
            Integer[] intArray = {1,2,3,4,5};
            String[] strings = {“a”,”b”,”c”,”d”};
            // Arrays.toString 返回指定数组内容的字符串表达形式
            // 直接迭代，输出 形式
            String intArrayString = Arrays.toString(intArray);
            String intArrayString1 = Arrays.toString(strings);
            // 检查数组中，是否包含某一个元素
            boolean b = Arrays.asList(strings).contains(“a”);
            boolean b1 = Arrays.asList(intArray).contains(1);

            // 复制数组，从 intAarry 数组复制 2 个元素
            Integer[] integer1 = Arrays.copyOf(intArray,2);
            //  复制数组，从 intAarry 数组 指定位置 2复制 到 结束位置 5
            Integer[] integer2 = Arrays.copyOfRange(intArray,2,5);
            // Arrays.toString 返回指定数组内容的字符串表达形式 ,输出
            String integers3 = Arrays.toString(integers1);
            String integers4 = Arrays.toString(integers2);

            // 方法块,输出检测内容 true , false
            void method(){
                System.out.println(b);
                System.out.println(b1);
            }
            public static void main(String[] args){
                // 实例化，调用方法
                ArrayDemo arrayDemo = new ArrayDemo();
                System.out.println(arrayDemo.intArrayString);
                System.out.println(arrayDemo.intArrayString1);
                // 输出方法块语句
                arrayDemo.method();
                // 输出复制数组
               System.out.println(arrayDemo.integers3);
               System.out.println(arrayDemo.integers4);
            }
        }

- `注：更多方法参考 API 文档 java.lang.util.Arrays`

     - 建议掌握的方法

        - asList()

        - copyOf()

        - copyOfRange()

        - sort()

        - toString()

### 二位数组

- 二维数组定义：

    type arrayName[ ][ ];

    type [ ][ ]arrayName;

    形式差别，根据自身习惯选择。

- 二维数组的初始化：

    - 静态初始化

        - int intArray`[` `] [` `]` = {{1,2},{3,4},{5,6,7}};

        - Java语言中，由于把二维数组看作是数组的数组，数组空间不是连续分配的，所以不要求二维数组每一维的大小相同。

    - 动态初始化

        - 直接为每一维分配空间，格式如下：

         arrayName = new type`[`arrayLength1`] [`arrayLength2`]`;

         int a[ ] [ ] = new int `[`2`][`3`]`;

    - 例：

            public class TwoArray1 {
                public static void main(String args[]) {
                    int a[][] = {{1,2},{3,4,5,6},{7,8,9}} ;
                    for(int i=0 ; i <a.length ; i++) {
                        for(int j=0 ; j<a[i].length ; j++) {
                            System.out.println("a[" + i + "][" + j + "]=" + a[i][j]);

                        }
                    }
                    //定义二维数组
                    int[ ] [ ] arr = {{1,2,3},{4,5,6,7,8},{9,10,11
            }};

                    //静态初始化
                    //打印出二维数组
                    // i 的长度 是数组个数的长度，为3， j 的长度是数组内的长度
                    for(int i = 0;i < arr.length;i++)
            {
                        for(int j = 0;j < arr[i].length;j++){
                            System.out.print(arr[i][j]+" ");

                        }
                        // 输出一列后就回车空格
                        System.out.println()
            ;

                    }
                }
            }
            运行结果：
            a[0][0]=1
            a[0][1]=2
            a[1][0]=3
            a[1][1]=4
            a[1][2]=5
            a[1][3]=6
            a[2][0]=7
            a[2][1]=8
            a[2][2]=9
            1 2 3
            4 5 6 7 8
            9 10 11

### 多维数组输出


        int[][][][][] ints1 = new int[3][2][3][4][5];
         for (int i = 0; i < ints1.length; i++) {
            for (int j = 0; j < ints1[i].length; j++) {
                for (int k = 0; k < ints1[i][j].length; k++) {
                    for (int l = 0; l < ints1[i][j][k].length; l++) {
                        for (int m = 0; m < ints1[i][j][k][l].length; m++) {
                            ints1[i][j][k][l][m] = i + j + k + l + m ;
                            System.out.print(ints1[i][j][k][l][m] + “\t");
                            }
                        System.out.println("--");            }
                }
            }
        }


### 游戏棋盘输出

        public class CheseboardGame {
            private static final char[] COLORS = {'红','黑','白','绿','黄','灰'};
            public static void main(String[] args) {
                char[][] square = new char[10][10];
                for (int i = 0; i < square.length; i++) {
                    for (int j = 0; j < square[i].length; j++) {
                        square[i][j] = COLORS[(int) (Math.random()*6)];
                        System.out.print(square[i][j] +"\t");
                    }
                    System.out.println();
                }
            }
        }
