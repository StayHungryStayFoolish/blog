---
layout:     post
title:      "Java 集合框架之 -- List"
subtitle:   "List 列表"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-14
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - ArrayList
    - LinkedList
    - Vector
    - Stack
    - 容量
---

### List 列表

- List 是一个`接口`,继承于 Collection

- 有序队列 `index`

    - 次序是 List 最主要的特点

- 元素以线性方式存储，集合中可以存放`重复`元素

- 可以存在多个 `null`

### List 接口主要实现类

- ArrayList : 代表长度可以改变得数组。可以对元素进行随机的访问，向ArrayList()中插入与删除元素的速度慢。

- LinkedList : 在实现中采用链表数据结构。插入和删除速度快，访问速度慢。实现了 Deque 接口，`先进先出`原则。

- Vector : 向量，可以实现自增长的对象数组。JDK 早起版本存在，与上边两个不同的是，Vector 是同步的，保证了线程的安全。

    - Stack : 堆栈，继承于 Vector，并进行扩展。采用`后进先出`原则。

### ArrayList 特性

- 初始容量 `10`

    - 如果溢出，扩容为原来的1.5倍。原容量为奇数时，扩容时，取两者较小值。

    - 没有 capacity 容量方法。需要使用反射机制。

    - 无 capacity ，Vector 有。

- 底层由数组实现

- 索引 `index`

- 允许对元素进行快速、随机访问，因为有`索引`

- 插入、删除开销`大`

    - 因为插入、删除需要移动改元素后边所有元素

    - 操作元素越靠前，开销越大，反之亦然。


### LinkedList 特性

- 底层由链表实现

- 对顺序访问进行了优化，但是随机访问较慢

    - 访问元素越靠前，开销越小，反之亦然

- 插入、删除数据开销`小`

    - 因为插入、删除任何元素，只需更改链表前后元素的指针指向即可（自行车链子）

- 因为没有索引，所以只能自己扩展几个关于 `first` `last` 方法装装样子咯。

    - addFirst()

    - addLast()

    - getFirst()

    - getLast()

    - removeFirst()

    - removeLast()

### Vector 特性

- 初始容量 10

    - 如果溢出，扩容为原来的 2 倍。

    - 有 capacity 方法

- 同步，安全性高

### Stack

- 原理类似弹匣

- 了解几个方法

    - peek() 查看堆栈顶部对象

    - pop() 移除堆栈顶部对象

    - push() 压入堆栈顶部

### 方法介绍

- List 继承于 Collection，所以拥有 Collection 所有方法

- Collection 接口主要方法

    - add()

    - clear()

    - contains()

    - equals()

    - isEmpty()

    - iterator() `必须使用 Iterator 来接收返回值`

    - remove()

    - removeAll()

    - size()

    - toArray() `返回此集合中所有元素的数组`

        - 无参使用 Object 接收返回值

        - 有参使用参数类型接收返回值 `集合和数组之间转换桥梁`

- List 扩展后

    - get(int index)

    - indexOf() 返回第一次出现指定元素索引，无返回 -1

    - lastIndexOf() 同上，相反

    - remove(int index) 移除一定索引，`返回移除元素`

    - remove(Object o) 移除指定元素，返回布尔值

    - set(int index,E element) 替换指定索引，`返回被替换的 E`

    - subList(fromIndex , toIndex） 返回子集合视图，`左开右闭，即包含起始，不包含结束`

- ArrayList 扩展 List 后

    - removeRange(int formIndex ,int toIndex) 移除列表中起始索引到结束索引之间的所有元素 `左开右闭`

- LinkedList 不再介绍，请查看 API

- Vector

    - setSize() 设定向量大小

- Stack 略


### 例

- List

        public class ListDemo{
        	public static void main(String []args){
        		//List list = method_Add();
        		//method_it(list);
        		//sop(list);
        		method_ArrayList();
        	}
        	public static void method_ArrayList(){
        		ArrayList al = new ArrayList();
        		sop(al.size());
        	}
        	public static List method_Add(){
        		List list = new ArrayList();
        		list.add("java1--->name");
        		list.add("java2--->name");
        		list.add("java3--->name");
        		list.add(2,"java4--->name");  //在制定位置插入
        		return list;
        	}
        	public static void method_it(List list){
        		//通过iteraror遍历元素
        		ListIterator li = list.listIterator();
        		while(li.hasNext()){
        			Object obj = li.next();
        			if(obj.equals("java3--->name"))
        				li.add("i love xy");
        			sop(obj);
        		}
        		while(li.hasPrevious()){
        				Object obj1 = li.previous();
        				sop("逆序--"+obj1);
        		}
        		/**此处会抛出ConcurrentModificationException异常
        		Iterator it = list.iterator();
        		while(it.hasNext()){
        			Object obj = it.next();
        			if(obj.equals("java3--->name")){
        				list.add("i love xuYan");
        			}
        			sop(obj);
        		}**/

        	}
        	public static void sop(Object obj){
        		System.out.println(obj);
        	}
        }

- Vector

        public class VectorDemo{
        	public static void main(String args[]){
        		Vector v = new Vector();
        		v.add("hello");
        		v.add("world");
        		v.add("hi");
        		v.add("java");
        		Enumeration en = v.elements();  //获取枚举类型的数据
        		while(en.hasMoreElements()){
        			System.out.println("遍历枚举类型的数据："en.nextElement());
        		}
        	}
        }

- LinkedList


         public class LinkedListDemo{
         	public static void main(String args[]){
         		LinkedList ll = new LinkedList();
         		ll.offerFirst("java1");
         		ll.offerFirst("java2");
         		ll.offerFirst("java3");
         		ll.offerFirst("java4");
         		sop(ll);
         	}
         	public static void sop(Object obj){
         		System.out.println(obj);
         	}
         }


- 去除ArrayList中的相同对象元素。即：姓名和年龄相同的步骤：

  1、构造Person类，定义姓名、年龄两个属性，重写equals方法。

  2、将Person对象存储到ArrayList集合中。

  3、将对象一个个的取出。

  4、定义一个新的集合，将就集合中的数据放入新集合，在此之前先判断新集合中是否存在该数据。


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
        public class ArrayListDemo{
        	public static void main(String args[]){
        		ArrayList al = new ArrayList();
        		//Person p = new Person();
        		al.add(new Person("lzl",18));
        		al.add(new Person("lzl1",18));
        		al.add(new Person("lzl2",18));
        		al.add(new Person("lzl3",18));
        		al.add(new Person("lzl",18));
        		al = sigleElements(al);
        		Iterator it = al.iterator();
        		while(it.hasNext()){
        			Person p = (Person)it.next();
        			sop(p.getName()+"---"+p.getAge());
        		}
        	}
        	public static void sop(Object obj){
        		System.out.println(obj);
        	}
        	/*
        		去除相同的元素
        	*/
        	public static ArrayList sigleElements(ArrayList al){
        		ArrayList newAl = new ArrayList();
        		Iterator it = al.iterator();
        		while((it.hasNext())){
        			Object obj = it.next();
        			//如果新链表中不存在P对象的元素，则添加。
        			if(!newAl.contains(obj)){
        				sop("---");
        				newAl.add(obj);
        			}
        		}
        		return newAl;
        	}
        }
