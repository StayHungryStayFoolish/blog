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


- TreeSet

  定义一个学生类，存入姓名、年龄，按照年龄排序


        public class SetDemo{
        	public static void main(String args[]){
        		TreeSet ts = new TreeSet();
        		ts.add(new Student("lzl",18));
        		ts.add(new Student("lzl",19));
        		ts.add(new Student("lzl",10));
        		ts.add(new Student("lzl",20));
        		ts.add(new Student("lml",20));
        		ts.add(new Student("lzl",20));
        		Iterator it = ts.iterator();
        		while(it.hasNext()){
        			Student s = (Student)it.next();
        			sop(s.getName()+"------"+s.getAge());
        		}
        	}
        	public static void sop(Object obj){
        		System.out.println(obj);
        	}
        }
        /**
        因为要将学生类按照年龄来排序，所以要实现Comparable接口，并
        覆写compareTo(Object obj)方法
        */
        class Student implements Comparable
        {
        	private String name ;
        	private int age;
        	public Student(){

        	}
        	public Student(String name,int age){
        		this.name = name;
        		this.age = age;
        	}
        	public int getAge(){
        		return this.age;
        	}
        	public String getName(){
        		return this.name;
        	}
        	/**
        	return：负整数、零或正整数，根据此对象是小于、等于还是大于指定对象。
        	*/
        	public int compareTo(Object obj){
        		if(!(obj instanceof Student))
        			throw new RuntimeException("不是学生类");
        		Student s = (Student)obj;
        		if(this.age > s.getAge())
        			return 1;
        		if(this.age == s.getAge()){
        			//年龄如果相同，比较姓名是否相同
        			return this.name.compareTo(s.getName());
        		}
        		return -1;
        	}
        }

     改变学生类的需求，要求让存储的学生类按照姓名的字母排序。

            public class TreeSetDemo{
            	public static void main(String args[]){
            		TreeSet ts = new TreeSet(new myCopara());
            		ts.add(new Student("lzl",18));
            		ts.add(new Student("lzl",19));
            		ts.add(new Student("lzl",10));
            		ts.add(new Student("lzl",12));
            		ts.add(new Student("lml",20));
            		ts.add(new Student("lzl",20));
            		ts.add(new Student("xy",20));
            		ts.add(new Student("as",100));
            		Iterator it = ts.iterator();
            		while(it.hasNext()){
            			Student s = (Student)it.next();
            			sop(s.getName()+"------"+s.getAge());
            		}
            	}
            	public static void sop(Object obj){
            		System.out.println(obj);
            	}
            }
            /**
            实现Comparator接口，并覆写int compare(T o1, T o2)
            */
            class myCopara implements Comparator{
            	public int compare(Object o1,Object o2){
            		if(!(o1 instanceof Student) || !(o2 instanceof Student))
            			throw new RuntimeException("不是学生类型");
            		Student s1 = (Student)o1;
            		Student s2 = (Student)o2;
            		int num = s1.getName().compareTo(s2.getName());
            		if(num == 0){
            			return new Integer(s1.getAge()).compareTo(new Integer(s2.getAge()));
            		}
            		return num;
            	}
            }
            class Student
            {
            	private String name ;
            	private int age;
            	public Student(){

            	}
            	public Student(String name,int age){
            		this.name = name;
            		this.age = age;
            	}
            	public int getAge(){
            		return this.age;
            	}
            	public String getName(){
            		return this.name;
            	}
            }


- 定义一堆字符串，要求按照字符串的长度大小来排序,如果字符串长度相同，那么按照字符串的字母顺序排序。


                    public class TreeSetDemo{
                    	public static void main(String args[]){
                    		TreeSet ts = new TreeSet(new myCopara());
                    		ts.add("abc");
                    		ts.add("abcd");
                    		ts.add("abcde");
                    		ts.add("abce");
                    		ts.add("fffff");
                    		ts.add("fffff");
                    	//	ts.add(2);
                    		Iterator it = ts.iterator();
                    		while(it.hasNext()){
                    			String s = (String)it.next();
                    			sop(s);
                    		}
                    	}
                    	public static void sop(Object obj){
                    		System.out.println(obj);
                    	}
                    }
                    /**
                    实现Comparator接口，并覆写int compare(T o1, T o2)
                    */
                    class myCopara implements Comparator{
                    	public int compare(Object o1,Object o2){
                    		if(!(o1 instanceof String) || !(o2 instanceof String))
                    			throw new RuntimeException("不是字符串类型");
                    		String s1 = (String)o1;
                    		String s2 = (String)o2;
                    		int size1 = s1.length();
                    		int size2 = s2.length();
                    		int num = new Integer(size1).compareTo(new Integer(size2));
                    		//如果长度相同，那么按照字符串的字母顺序排列
                    		if(num == 0){
                    			//System.out.println(s1+"----"+s2);
                    			return s1.compareTo(s2);
                    		}
                    		return num;
                    	}
                    }
