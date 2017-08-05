---
layout:     post
title:      "Java 集合框架之 -- Set"
subtitle:   "Set 集合"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-14
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - HashSet
    - LinkedHashSet
    - TreeSet

---

## Set 集合

- Set 是一个`接口`，继承于 Collection

- 无序

- 不允许重复元素，只允许有一个 Null 存在。

## Set 主要实现类

- HashSet `无序`

    - LinkedHast 继承于 HashSet 以 `元素插入顺序排序`

- TreeSet 按元素`自然顺序排序`，因为实现了 NavigableSet 接口


### HashSet 特性

- 使用 HashMap 来存储元素，因为 HashSet 是 HashMap 的一个实例。

- 无序

- 效率高

- 不同步，多线程不安全

- 初始容量16，加载因子是0.75

- 构造器支持设置初始容量

- 不支持快速随机遍历，只能通过迭代器进行遍历 iterator 。

### LinkedHashSet 特性

- 支持以元素插入顺序进行维护的`链表`结构

- 允许以`插入`的顺序在集合器中迭代

- 按元素`插入`顺序进行排序

- 初始容量16，加载因子是0.75

- 不同步，多线程不安全

- 构造器支持设置初始容量

- 不支持快速随机遍历，只能通过迭代器进行遍历 iterator 。

### TreeSet

- 红黑树结构

- 实现 NavigableSet，所以支持元素的`自然顺序`排序

- 不支持快速随机遍历，只能通过迭代器进行遍历 iterator 。

- 不同步，多线程不安全


### 方法介绍

- Set 方法

    - add(E e)

    - addAll(Collection<? extends E> c) 添加一个集合到此 set 中

    - clear() 移除所有元素

    - contains(Object o) 是否包含

    - containsAll(Collection<?> c) 是否包含此集合

    - equals()

    - isEmpty()

    - iterator() 使用 Iterator 来接受此迭代

    - remove(Object o)  移除指定元素

    - removeAll(Collection<?> c) 移除 set 中指定的collection 中的额元素

    - retainAll() 仅保留 Set 指定元素

    - size() 返回 set 容量

    - toArray() `返回此集合中所有元素的数组`

         - 无参使用 Object 接收返回值

         - 有参使用参数类型接收返回值 `集合和数组之间转换桥梁`

- HashSet 扩展方法

    - clone() 返回 HashSet 实例的浅表副本，但不赋值

- LinkedHashSet 含有以上方法

- TreeSet

    - ceiling(E e) 返回大于指定元素的最小元素，无则返回 null

    - comparator() 返回元素进行排序的比较器，使用 Comparator 来接收

    - first() 返回当前第一个元素（也是最低的）

    - floor() 返回小于指定元素的最大元素，无则返回 null

    - last() 返回当前最后一个元素（也是最高的）

    - lower() 返回小于指定元素的最大元素，无则返回 null

    - pollFirst() 移除第一个，set 空则返回 null

    - pollLast() 移除第一个，set 空则返回 null

    - subSet(E fromElement, E toElement) 返回 set 视图，`左开右闭`


### 例：

- HashSet


        public class SetDemo{
        	public static void main(String args[]){
        		HashSet hs = new HashSet();
        		hs.add(new Person("lzl",18));
        		hs.add(new Person("lzl",18));
        		hs.add(new Person("hhh",18));
        		hs.add(new Person("lzl",18));
        		Iterator it = hs.iterator();
        		while(it.hasNext()){
        			Person p = (Person)it.next();
        			sop(p.getName()+"-------"+p.getAge());
        		}
        	}
        	public static void sop(Object obj){
        		System.out.println(obj);
        	}
        }
        class Person{
        	private String name ;
        	private int age;
        	public Person(){

        	}
        	public Person(String name,int age){
        		this.name = name;
        		this.age = age;
        	}
        	public int getAge(){
        		return this.age;
        	}
        	public String getName(){
        		return this.name;
        	}
        	//覆写hashCode()方法，保证hashCode具有唯一性
        	public int hashCode(){
        		System.out.println("hashCode---"+this.name.hashCode()*age);
        		return this.name.hashCode()*age;
        	}
        	//因为要比较的是Person类中的name和age值，所以重写Object类的equals方法，
        	public boolean equals(Object obj){
        		//如果传入的对象不是Person类，直接返回false
        		if(!(obj instanceof Person))
        			return false;
        		//否则强转成Person类
        		Person p = (Person)obj;
        		//返回name和age的比较值。
        		return this.name.equals(p.getName()) && this.age == p.getAge();
        	}
        }
