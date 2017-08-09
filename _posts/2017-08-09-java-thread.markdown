---
layout:     post
title:      "Java 线程 "
subtitle:   "进程、线程"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-28
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 进程
    - 线程
    - synchronized
---

### 进程、线程

- `进程是一个内存中运行的应用程序。一个进程中可以启动多个线程`

- `线程是指进程中的一个执行流程，一个进程中可以运行多个线程。`

`即：进程执行的是应用程序，线程是进程内部的一个执行序列`

### 线程分类

- 非守护线程（用户线程）

    - 用户自己创建的，用来运行应用程序。

- 守护线程

    - 只要当前 JVM 实例中，存在任何一个非守护线程没有结束，守护线程就不会停止工作。
        只有当最后一个非守护线程结束时，守护线程才会随着 JVM 一起结束工作。

    - 最典型应用：GC（垃圾回收期）

        - 也正是因为 GC 的机制存在，Java 不会出现内存泄漏。

### 多线程的实现

1.扩展 Thread 类

2.实现 Runnable 接口

- `一个类只能继承一个 Thread，这是 Thread 的局限，推荐使用 Runnable 接口`

- `Runnable 的好处在于`

    避免点继承的局限，一个类可以实现多个接口。

    适合资源的共享

### 例：

- 以售票为例

    - Thread

            class MyThread extends Thread{
                private int ticket=10;
                public void run(){
                    for(int i=0;i<20;i++){
                        if(this.ticket>0){
                        System.out.println("卖票：ticket"+this.ticket--);
                        }
                    }
                }
            };

            public class ThreadTicket {
                public static void main(String[] args) {
                    MyThread mt1=new MyThread();
                    MyThread mt2=new MyThread();
                    MyThread mt3=new MyThread();
                    mt1.start();//每个线程都各卖了10张，共卖了30张票
                    mt2.start();//但实际只有10张票，每个线程都卖自己的票
                    mt3.start();//没有达到资源共享
                }
            }

    - Runnable

