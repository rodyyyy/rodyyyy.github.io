---
layout: post
title: Collection和Arrays的部分方法
author: Chris Rody
---

### 集合和数组的区别

[参考博文](<https://blog.csdn.net/qq_27088383/article/details/50468779>)

> ```
> 一、数组声明了它容纳的元素的类型，而集合不声明。
> 二、数组是静态的，一个数组实例具有固定的大小，一旦创建了就无法改变容量了。而集合是可以动态扩展容量，可以根据需要动态改变大小，集合提供更多的成员方法，能满足更多的需求。
> 三、数组不论是效率还是类型检查都是最好的。
> 
> 1.数组是大小固定的,一旦创建无法扩容;集合大小不固定,
> 2.数组的存放的类型只能是一种,集合存放的类型可以不是一种(不加泛型时添加的类型是Object);
> 3.数组是java语言中内置的数据类型,是线性排列的,执行效率或者类型检查(不懂),都是最快的.
> ```
>
> **ArrayList就是基于数组创建的容器类.**

~~~
数组Array和集合的区别：
 
(1)数组是大小固定的，并且同一个数组只能存放类型一样的数据（基本类型/引用类型）
 
(2)JAVA集合可以存储和操作数目不固定的一组数据。 (3)若程序时不知道究竟需要多少对象，需要在空间不足时自动扩增容量，则需要使用容器类库，array不适用。
 
联系：使用相应的toArray()和Arrays.asList()方法可以回想转换。
 
一.集合的体系结构：
 
List、Set、Map是这个集合体系中最主要的三个接口。 List和Set继承自Collection接口。 Map也属于集合系统，但和Collection接口不同。
 
Set不允许元素重复。HashSet和TreeSet是两个主要的实现类。Set 只能通过游标来取值，并且值是不能重复的。
 
List有序且允许元素重复。ArrayList、LinkedList和Vector是三个主要的实现类。 ArrayList 是线程不安全的， Vector 是线程安全的，这两个类底层都是由数组实现的 LinkedList 是线程不安全的，底层是由链表实现的
 
Map 是键值对集合。其中key列就是一个集合，key不能重复，但是value可以重复。 HashMap、TreeMap和Hashtable是Map的三个主要的实现类。 HashTable 是线程安全的，不能存储 null 值 HashMap 不是线程安全的，可以存储 null 值
 
二.List和ArrayList的区别
 
1.List是接口，List特性就是有序,会确保以一定的顺序保存元素.
 
ArrayList是它的实现类,是一个用数组实现的List.
 
Map是接口,Map特性就是根据一个对象查找对象.
 
HashMap是它的实现类,HashMap用hash表实现的Map,就是利用对象的hashcode(hashcode()是Object的方法)进行快速散列查找.(关于散列查找,可以参看<<数据结构>>)
 
2.一般情况下,如果没有必要,推荐代码只同List,Map接口打交道.
 
比如:List list = new ArrayList();
 
这样做的原因是list就相当于是一个泛型的实现,如果想改变list的类型,只需要:
 
List list = new LinkedList();//LinkedList也是List的实现类,也是ArrayList的兄弟类
 
这样,就不需要修改其它代码,这就是接口编程的优雅之处.
 
另外的例子就是,在类的方法中,如下声明:
 
private void doMyAction(List list){}
 
这样这个方法能处理所有实现了List接口的类,一定程度上实现了泛型函数.
 
3.如果开发的时候觉得ArrayList,HashMap的性能不能满足你的需要,可以通过实现List,Map(或者Collection)来定制你的自定义类.

~~~

![md文件名格式](https://github.com/rodyyyy/rodyyyy.github.io/raw/master/images/a1.PNG)

![md文件名格式](https://github.com/rodyyyy/rodyyyy.github.io/raw/master/images/a2.PNG)

```java
int[] m = { 1, 2, 3 };
String[] strings = { "aaa", "bbb" };
List<String> list = new ArrayList<String>();
List<Integer> lists = new ArrayList<Integer>();
List<Map<String, Object>> list2 = new ArrayList<Map<String,Object>>();
List<City> listcity = new ArrayList<City>();
```



### Collections 工具类和 Arrays 工具类常见方法

#### Collections

Collections 工具类常用方法:

1. 排序
2. 查找,替换操作
3. 同步控制(不推荐，需要线程安全的集合类型时请考虑使用 JUC 包下的并发集合)

#####  1，排序操作

```java
void reverse(List list)//反转
void shuffle(List list)//随机排序
void sort(List list)//按自然排序的升序排序
void sort(List list, Comparator c)//定制排序，由Comparator控制排序逻辑
void swap(List list, int i , int j)//交换两个索引位置的元素
void rotate(List list, int distance)//旋转。当distance为正数时，将list后distance个元素整体移到前面。当distance为负数时，将 list的前distance个元素整体移到后面。
```

**示例代码:**

```java
     ArrayList<Integer> arrayList = new ArrayList<Integer>();
		arrayList.add(-1);
		arrayList.add(3);
		arrayList.add(3);
		arrayList.add(-5);
		arrayList.add(7);
		arrayList.add(4);
		arrayList.add(-9);
		arrayList.add(-7);
		System.out.println("原始数组:");
		System.out.println(arrayList);
		// void reverse(List list)：反转
		Collections.reverse(arrayList);
		System.out.println("Collections.reverse(arrayList):");
		System.out.println(arrayList);
		
		 
		Collections.rotate(arrayList, 4);
		System.out.println("Collections.rotate(arrayList, 4):");
		System.out.println(arrayList);
		
		// void sort(List list),按自然排序的升序排序
		Collections.sort(arrayList);
		System.out.println("Collections.sort(arrayList):");
		System.out.println(arrayList);

		// void shuffle(List list),随机排序
		Collections.shuffle(arrayList);
		System.out.println("Collections.shuffle(arrayList):");
		System.out.println(arrayList);

		// 定制排序的用法
		Collections.sort(arrayList, new Comparator<Integer>() {

			@Override
			public int compare(Integer o1, Integer o2) {
				return o2.compareTo(o1);
			}
		});
		System.out.println("定制排序后：");
		System.out.println(arrayList);
```

##### 2，查找,替换操作

```java
int binarySearch(List list, Object key)//对List进行二分查找，返回索引，注意List必须是有序的
int max(Collection coll)//根据元素的自然顺序，返回最大的元素。 类比int min(Collection coll)
int max(Collection coll, Comparator c)//根据定制排序，返回最大元素，排序规则由Comparatator类控制。类比int min(Collection coll, Comparator c)
void fill(List list, Object obj)//用指定的元素代替指定list中的所有元素。 
int frequency(Collection c, Object o)//统计元素出现次数
int indexOfSubList(List list, List target)//统计targe在list中第一次出现的索引，找不到则返回-1，类比int lastIndexOfSubList(List source, list target).
boolean replaceAll(List list, Object oldVal, Object newVal), 用新元素替换旧元素
```

**示例代码：**

```java
		ArrayList<Integer> arrayList = new ArrayList<Integer>();
		arrayList.add(-1);
		arrayList.add(3);
		arrayList.add(3);
		arrayList.add(-5);
		arrayList.add(7);
		arrayList.add(4);
		arrayList.add(-9);
		arrayList.add(-7);
		ArrayList<Integer> arrayList2 = new ArrayList<Integer>();
		arrayList2.add(-3);
		arrayList2.add(-5);
		arrayList2.add(7);
		System.out.println("原始数组:");
		System.out.println(arrayList);

		System.out.println("Collections.max(arrayList):");
		System.out.println(Collections.max(arrayList));

		System.out.println("Collections.min(arrayList):");
		System.out.println(Collections.min(arrayList));

		System.out.println("Collections.replaceAll(arrayList, 3, -3):");
		Collections.replaceAll(arrayList, 3, -3);
		System.out.println(arrayList);

		System.out.println("Collections.frequency(arrayList, -3):");
		System.out.println(Collections.frequency(arrayList, -3));

		System.out.println("Collections.indexOfSubList(arrayList, arrayList2):");
		System.out.println(Collections.indexOfSubList(arrayList, arrayList2));

		System.out.println("Collections.binarySearch(arrayList, 7):");
		// 对List进行二分查找，返回索引，List必须是有序的
		Collections.sort(arrayList);
		System.out.println(Collections.binarySearch(arrayList, 7));
```

##### 3，同步控制

Collectons提供了多个`synchronizedXxx()`方法·，该方法可以将指定集合包装成线程同步的集合，从而解决多线程并发访问集合时的线程安全问题。

我们知道 HashSet，TreeSet，ArrayList,LinkedList,HashMap,TreeMap 都是线程不安全的。Collections提供了多个静态方法可以把他们包装成线程同步的集合。

**最好不要用下面这些方法，效率非常低，需要线程安全的集合类型时请考虑使用 JUC 包下的并发集合。**

方法如下：

```java
synchronizedCollection(Collection<T>  c) //返回指定 collection 支持的同步（线程安全的）collection。
synchronizedList(List<T> list)//返回指定列表支持的同步（线程安全的）List。 
synchronizedMap(Map<K,V> m) //返回由指定映射支持的同步（线程安全的）Map。
synchronizedSet(Set<T> s) //返回指定 set 支持的同步（线程安全的）set。 
```

#### Arrays
1. 排序 : `sort()`
2. 查找 : `binarySearch()`
3. 比较: `equals()`
4. 填充 : `fill()`
5. 转列表:  `asList()`
6. 转字符串 : `toString()`

##### 1，排序 : `sort()`

```java
		// *************排序 sort****************
		int a[] = { 1, 3, 2, 7, 6, 5, 4, 9 };
		// sort(int[] a)方法按照数字顺序排列指定的数组。
		Arrays.sort(a);
		System.out.println("Arrays.sort(a):");
		for (int i : a) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		// sort(int[] a,int fromIndex,int toIndex)按升序排列数组的指定范围
		int b[] = { 1, 3, 2, 7, 6, 5, 4, 9 };
		Arrays.sort(b, 2, 6);
		System.out.println("Arrays.sort(b, 2, 6):");
		for (int i : b) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		int c[] = { 1, 3, 2, 7, 6, 5, 4, 9 };
		// parallelSort(int[] a) 按照数字顺序排列指定的数组。同sort方法一样也有按范围的排序
		Arrays.parallelSort(c);
		System.out.println("Arrays.parallelSort(c)：");
		for (int i : c) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		// parallelSort给字符数组排序，sort也可以
		char d[] = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		Arrays.parallelSort(d);
		System.out.println("Arrays.parallelSort(d)：");
		for (char d2 : d) {
			System.out.print(d2);
		}
		// 换行
		System.out.println();

```

在做算法面试题的时候，我们还可能会经常遇到对字符串排序的情况,`Arrays.sort()` 对每个字符串的特定位置进行比较，然后按照升序排序。

```java
String[] strs = { "abcdehg", "abcdefg", "abcdeag" };
Arrays.sort(strs);
System.out.println(Arrays.toString(strs));//[abcdeag, abcdefg, abcdehg]
```

##### 2，查找 : `binarySearch()`

```java
		// *************查找 binarySearch()****************
		char[] e = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		System.out.println("Arrays.binarySearch(e, 'c')：");
		int s = Arrays.binarySearch(e, 'c');
		System.out.println("字符c在数组的位置：" + s);
```

##### 3，比较: `equals()`

```java
	// *************比较 equals****************
        char[] e = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		char[] f = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		/*
		 * 元素数量相同，并且相同位置的元素相同。 另外，如果两个数组引用都是null，则它们被认为是相等的 。
		 */
		// 输出true
		System.out.println("Arrays.equals(e, f):" + Arrays.equals(e, f));
```

##### 4，填充 : `fill()`

```java
		// *************填充fill(批量初始化)****************
		int[] g = { 1, 2, 3, 3, 3, 3, 6, 6, 6 };
		// 数组中所有元素重新分配值
		Arrays.fill(g, 3);
		System.out.println("Arrays.fill(g, 3)：");
		// 输出结果：333333333
		for (int i : g) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		int[] h = { 1, 2, 3, 3, 3, 3, 6, 6, 6, };
		// 数组中指定范围元素重新分配值
		Arrays.fill(h, 0, 2, 9);
		System.out.println("Arrays.fill(h, 0, 2, 9);：");
		// 输出结果：993333666
		for (int i : h) {
			System.out.print(i);
		}
```

##### 5，转列表 `asList()`

```java
		// *************转列表 asList()****************
		/*
		 * 返回由指定数组支持的固定大小的列表。
		 * （将返回的列表更改为“写入数组”。）该方法作为基于数组和基于集合的API之间的桥梁，与Collection.toArray()相结合 。
		 * 返回的列表是可序列化的，并实现RandomAccess 。
		 * 此方法还提供了一种方便的方式来创建一个初始化为包含几个元素的固定大小的列表如下：
		 */
		List<String> stooges = Arrays.asList("Larry", "Moe", "Curly");
		System.out.println(stooges);
```

##### 6，转字符串 `toString()`

```java
        // *************转字符串 toString()****************
        /*
         * 返回指定数组的内容的字符串表示形式。
         */
        char[] k = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
        System.out.println(Arrays.toString(k));// [a, f, b, c, e, A, C, B]
```

##### 7，复制 `copyOf()`

```java
		// *************复制 copy****************
		// copyOf 方法实现数组复制,h为数组，6为复制的长度
        int[] h = { 1, 2, 3, 3, 3, 3, 6, 6, 6, };
		int i[] = Arrays.copyOf(h, 6);
		System.out.println("Arrays.copyOf(h, 6);：");
		// 输出结果：123333
		for (int j : i) {
			System.out.print(j);
		}
		// 换行
		System.out.println();
		// copyOfRange将指定数组的指定范围复制到新数组中
		int j[] = Arrays.copyOfRange(h, 6, 11);
		System.out.println("Arrays.copyOfRange(h, 6, 11)：");
		// 输出结果66600(h数组只有9个元素这里是从索引6到索引11复制所以不足的就为0)
		for (int j2 : j) {
			System.out.print(j2);
		}
		// 换行
		System.out.println();
```

