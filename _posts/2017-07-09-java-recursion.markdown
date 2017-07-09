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

        public class Prime {
            public void get(int n) {
                for (int i = 2; i < n + 1; i++) {
                    if (n % i == 0) {
                        if (i == n) {
                            System.out.print(i);
                            } else {
                            System.out.print(i + " * ");
                            get(n / i); // 递归算法
                       }
                        break;
                     }
                }
            }

            public static void main(String[] args) {
                // 10 = 2*5
                // 100 = 2*2*5*5
                // 1000 = 2*2*2*5*5*5
               // Ctrl + Alt + T
                Prime prime = new Prime();
                int n = 10000;
                System.out.print(n + " = ");
                prime.get(n);
             }
        }

-
  将一个正整数分解质因数。例如：输入90，打印出90=2*3*3*5。
  假设 n == 90，
  当 n 进入循环时，
  先进行条件，当 n % i == 0，进行判断，
  n 是否等于 i ，如果 n == i，则证明不能再分解，直接输出
  n 不等于 i ，进入 else，输出刚才的 i ，继续调用 get( n / i ) 方法
  然后 break 跳出循环。
  n 再次进入for 循环 , 注意：此时的 n 是 get( n / i) 后的 值
  然后继续判断，直到 n == i ，输出最后一个质因数。

### 求1+2!+3!+…+20!的和

- 例：

            public class Factorial {
                long sum;
                public long factorial (long n){
                    if (n == 1) {
                        return 1;
                        } else {
                        return n* factorial(n - 1); // 阶乘
                    }
                }
                public void getSum(){
                    for (int i = 1; i < 21; i++) {
                        sum += factorial(i);
                    }
                    System.out.println(sum);
                }
                public static void main(String[] args) {
                    Factorial factorial = new Factorial();
                    factorial.getSum();
                }
            }