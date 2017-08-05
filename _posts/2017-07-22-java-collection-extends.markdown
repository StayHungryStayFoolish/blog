---
layout:     post
title:      "Java 集合框架之 -- 扩展"
subtitle:   "各种异同"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-14
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 容量
    - 结构
    - 排序
---


### Collection、Map

<div>
    <img src="https://github.com/StayHungryStayFoolish/stayhungrystayfoolish.github.io/blob/master/img/java/collection.jpg?raw=true" />
</div>


||Collection|Map|备注|
|---|:---:|:---:|:---:|
|结构|每个位置只存一个元素，允许 null 存在|Key-Value结构，Key不允许 重复|Map 像小型数据库|
|形式|元素的集合|元素映射||

### List、Set

||List|Set|备注|
|---|:---:|:---:|:---:|
|结构|线性结构容器|零散不重复容器||
|元素|元素可以重复，多个 null|不可以重复，只允许一个 null||

### ArrayList、LinkedList

||AarrayList|LinkedList|备注|
|---|:---:|:---:|:---:|
|结构|数组形式|链表形式||
|索引|有`index`|无||
|顺序|有序|无序||
|访问|`快`根据索引随机访问|`慢`支持首尾||
|插入、删除|慢|快|ArrayList需要移动，LinkedList 只需改变前后指针指向|
|场景|快速随机访问|频繁操作数据||
|内存|相对少|更占用|因为 ArrayList 是索引，一个节点一个引用，LinkedList一个节点两个引用，分别指向前、后元素|

### HashSet、LinkedHashSet、TreeSet
||HashSet|LinkedHashSet|TreeSet|备注|
|---|:---:|:---:|:---:|:---:|
|容量|16|16|无||
|次序|无序|插入顺序|自然顺序|TreeSet 实现 NavigableSet接口|

### 初始容量、扩容、同步

|接口|实现类|初始容量|扩容|capacity|同步|备注|
|---|:---:|:---:|:---:|:---:|:---:|:---:|
|`List`|ArrayList|10|1.5倍|无|NO|原容量取0.5有奇数时，选较小值|
||LinkedList|※|API无说明|无|NO|
||Vector|10|2倍|`有`|`YES`|||
|`Set`|HashSet|16|0.75|无|NO||
||HashTable|11|0.75|无|YES||
||LinkedHashSet|16|0.75|无|NO||
||TreeSet|※|※|无|NO|红-黑树结构|
|`Map`|Hashmap|16|0.75|无|NO||
||LinkedHashMap|16|0.75|无|NO|底层使用 Hashtable 实现|
||TreeMap|※|※|无|NO|红-黑树结构|

### Array、ArrayList

|数据类型|Array 数组|ArrayList 集合|备注|
|---|:---:|:---:|:---:|
|基本类型|YES|NO||
|对象类型|YES|YES||
|大小|固定|动态|数组初始化、声明、创建是一体的，不可分割|
|拆箱、装箱|处理基本数据类型快|处理固定大小的基本数据类型慢|ArrayList y要拆装箱|
|属性|length|size()方法，无 length 属性||

### HashMap、Hashtable

||HashMap|Hashtable|备注|
|---|:---:|:---:|:---:|
|null|键值都可以是null|键值都不允许||
|同步|NO|YES||
|适用场景|单线程|多线程||

### 关于多线程使用非线程的安全问题

- Collections 的 synchronizedList() 方法，可以转换为线程安全的容器。

- 装潢模式

    - 将已有对象传入另一个类的构造器，然后创建新对象，以此来增加新功能。


### 例：

- Map 扩展

    例子：一个公司类，包括人力资源部门和技术部门。每个部门包括姓名和年龄

    要求存入到map集合中。

    步骤：

    利用嵌套的Map集合

    第一个map集合存储公司部门和HashMap<String,String>

    HashMap<String,String> 中存储对应的部门人姓名和年龄

    Map<String,HashMap<String,Integer>> company = Map<String,HashMap<String,String>>
    HashMap


            public class MapDemo2{
            	public static void main(String []args){
            		Map<String,HashMap<String,Integer>> company = new HashMap<String,HashMap<String,Integer>>();
            		HashMap<String,Integer> renli = new HashMap<String,Integer>();
            		HashMap<String,Integer> jishu = new HashMap<String,Integer>();
            		company.put("renli",renli);
            		company.put("jishu",jishu);

            		renli.put("liu",18);
            		renli.put("li",19);

            		jishu.put("xu",18);
            		jishu.put("wang",19);
            		Set<String> keySet = company.keySet();
            		Iterator<String> it = keySet.iterator();
            		while(it.hasNext()){
            			String bumen = it.next();
            			System.out.println("公司部门："+bumen);
            			HashMap<String,Integer> hs = company.get(bumen);
            			getInfo(hs);
            		}

            	}
            	public static void getInfo(HashMap<String,Integer> hashMap){
            		Set<Map.Entry<String,Integer>> entrySet = hashMap.entrySet();
            		Iterator<Map.Entry<String,Integer>> it = entrySet.iterator();
            		while(it.hasNext()){
            			Map.Entry<String,Integer> me = it.next();
            			String name = me.getKey();
            			Integer age = me.getValue();
            			System.out.println("name:"+name+" age:"+age);
            		}
            	}
            }

    给出一段字符串，要求输出字符串中每个字符以及字符出现的次数。并且按照字符出现的次数又打到进行排序

    例如 输入:"jjjaaabccd"

    输出: a(3)j(3)c(2)b(1)d(1)

    算法实现：

    1、将字符串转换成字符数组

    2、定义一个map集合，因为要实现某种顺序，所以要用TreeMap()集合

    3、将字符数组与map集合中进行匹对， 如果map中不存在该字符，将字符存入到map的key值中，并将value值+1， 如果存在该字符，将value值取出+1

    4、将结果存入到map集合中，并且创建一个比较器实现Comparator方法，按照Value值的大小来进行比较

    5、按照格式遍历输出字符串


            public class TreeMapDemo{
            	public static void main(String []args){
            		System.out.println("请输入字符串");
            		Scanner input = new Scanner(System.in);
            		String str =  input.next();
            	//	String str = "aabbbbbccda";
            	char[] ch = str.toCharArray();
            	Map<Character,Integer> map = getChar(ch);
            	if(map.isEmpty())
            		System.out.println("空字符");
            	valueSort(map);
            	}
            	/**
            	 * 按照value值进行排序
            	 * 思路，将Map集合转换成List集合，利用Collections.sort(list,Comparator<>)方法进行排序
            	 * @param map
            	 */
            	public static void valueSort(Map<Character,Integer> map){
            		System.out.println("--------");
            		List<Entry<Character, Integer>> list = new ArrayList<Map.Entry<Character,Integer>>(map.entrySet());
            		Collections.sort(list,new Comparator<Map.Entry<Character, Integer>>() {
            			@Override
            			public int compare(Entry<Character, Integer> o1,
            					Entry<Character, Integer> o2) {
            				return o2.getValue() - o1.getValue();
            			}
            		});
            		Iterator<Entry<Character, Integer>> it = list.iterator();
            		while(it.hasNext()){
            			Map.Entry<Character,Integer> me = it.next();
            			char c = me.getKey();
            			int v = me.getValue();
            			System.out.println(c+"("+v+")");
            		}
            	}
            	public static Map<Character,Integer> getChar(char[] ch){
            		Map<Character,Integer> map = new TreeMap<Character,Integer>();
            		for(int i=0;i<ch.length;i++){
            			if(ch[i]<'a'&&ch[i]>'z'||ch[i]<'A'&&ch[i]>'Z')
            				continue;
            			Integer value = map.get(ch[i]);  //通过key值获取map中存入的value值
            			if(value == null){  //如果value为空，表示map中不存在该字符，我们将它存入到map中
            				map.put(ch[i],1);
            			}else{ //如果不为空，表示map中已经存在该字符，我们将value值+1在存入到map中
            				value++;
            				map.put(ch[i],value);
            			}
            		}
            		return map;
            	}
            }