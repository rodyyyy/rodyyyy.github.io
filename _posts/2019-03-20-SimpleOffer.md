---
layout: post
title: 算法之路
author: Chris Rody
---

算法记录

##  算法SE

### 1,二维数组的行和列

```java
int [][] array
//rows：array.length
//columes：array[0].length
//length是数组的一种属性，不用加（）
```

### 2,ArrayList总结

> ArrayList：动态数组类，ArrayList对象既有数组的特征，也有链表的特征；可以随时从中添加或者删除元素，ArrayList实现了接口类，可以动态改变大小
>
> Array：数组是静态的，数组被初始化后，长度不能改变
>
> 使用区分：当我们不知道到底有多少个数据元素的时候，就可使用ArrayList；如果知道数据集合有多少个元素，就用数组

``` java
ArrayList<String> list = new ArrayList<String>();//创建一个空的数组链表，用来存放String类型的对象
ArrayList<Integer> list = new ArrayList<Integer>(7);//创建一个指定初始容量的数组链表
```

* **ArrayList类只支持对象类型，不支持基础数据类型—>ArrayList对象只能存放对象，不能存放基础数据类型的数据。**

> `ArrayList常用方法`
>
> boolean add(Element e) //增加指定元素到链表尾部
>
> void add(int index, Element e) //增加指定元素到链表指定位置
>
> void clear() //从链表中删除所有元素
>
> E remove(int index) //删除链表中指定位置的元素
>
> protected void removeRange(int start, int end) //删除链表中从某一个位置开始到某一个位置结束的元素
>
> E get(int index) //获取链表中指定位置处的元素
>
> Object[] toArray() //获取一个数组，数组中所有元素是链表中的元素.（即将链表转换为一个数组）
>
> boolean contains(Object o) //如果链表包含指定元素，返回true
>
> int indexOf(Object o) //返回元素在链表中第一次出现的位置，如果返回-1，表示链表中没有这个元素
>
> int lastIndexOf(Object o) //返回元素在链表中最后一次出现的位置，如果返回-1，表示链表中没有这个元素
>
> boolean isEmpty() //返回true表示链表中没有任何元素
>
> int size() //返回链表长度（链表包含元素的个数）

``` java
//ArrayList使用实例
import java.util.*;

public class ArrayListExamples {

    public static void main(String args[]) {
        // 创建一个空的数组链表对象list，list用来存放String类型的数据
        ArrayList<String> list = new ArrayList<String>();

        // 增加元素到list对象中
        list.add("Item1");
        list.add("Item2");
        list.add(2, "Item3"); // 此条语句将会把“Item3”字符串增加到list的第3个位置。
        list.add("Item4");

        // 显示数组链表中的内容
        System.out.println("The arraylist contains the following elements: "
                + list);

        // 检查元素的位置
        int pos = list.indexOf("Item2");
        System.out.println("The index of Item2 is: " + pos);

        // 检查数组链表是否为空
        boolean check = list.isEmpty();
        System.out.println("Checking if the arraylist is empty: " + check);

        // 获取链表的大小
        int size = list.size();
        System.out.println("The size of the list is: " + size);

        // 检查数组链表中是否包含某元素
        boolean element = list.contains("Item5");
        System.out
                .println("Checking if the arraylist contains the object Item5: "
                        + element);

        // 获取指定位置上的元素
        String item = list.get(0);
        System.out.println("The item is the index 0 is: " + item);

        // 遍历arraylist中的元素

        // 第1种方法: 循环使用元素的索引和链表的大小
        System.out
                .println("Retrieving items with loop using index and size list");
        for (int i = 0; i < list.size(); i++) {
            System.out.println("Index: " + i + " - Item: " + list.get(i));
        }

        // 第2种方法:使用foreach循环
        System.out.println("Retrieving items using foreach loop");
        for (String str : list) {
            System.out.println("Item is: " + str);
        }

        // 第三种方法:使用迭代器
        // hasNext(): 返回true表示链表链表中还有元素
        // next(): 返回下一个元素
        System.out.println("Retrieving items using iterator");
        for (Iterator<String> it = list.iterator(); it.hasNext();) {
            System.out.println("Item is: " + it.next());
        }

        // 替换元素
        list.set(1, "NewItem");
        System.out.println("The arraylist after the replacement is: " + list);

        // 移除元素
        // 移除第0个位置上的元素
        list.remove(0);

        // 移除第一次找到的 "Item3"元素
        list.remove("Item3");

        System.out.println("The final contents of the arraylist are: " + list);

        // 转换 ArrayList 为 Array
        String[] simpleArray = list.toArray(new String[list.size()]);
        System.out.println("The array created after the conversion of our arraylist is: "
                        + Arrays.toString(simpleArray));
    }
}
```

* **ArrayList有三种遍历方式**

```java
//迭代器遍历
Iterator<Integer> it = arrayList.iterator();
while(it.hasNext()){
    System.out.print(it.next() + " ");
}

//索引值遍历
for(int i = 0; i < arrayList.size(); i++){
   System.out.print(arrayList.get(i) + " ");
}

//for循环遍历
for(Integer number : arrayList){
   System.out.print(number + " ");
}
//遍历效率：索引值最高，for循环次之，迭代器最低
```

* **toArray的使用**

> 当我们调用ArrayList中的 toArray()，遇到java.lang.ClassCastException异常，这是由于toArray() 返回的是 Object[] 数组
>
> 将 Object[] 转换为其它类型(如，将Object[]转换为的Integer[])则会抛出java.lang.ClassCastException异常，因为Java不支持向下转型 

```java
 // toArray用法
 // 第一种方式(最常用)
 Integer[] integer = arrayList.toArray(new Integer[0]);

 // 第二种方式(容易理解)
 Integer[] integer1 = new Integer[arrayList.size()];
 arrayList.toArray(integer1);

 // 抛出异常，java不支持向下转型
 //Integer[] integer2 = new Integer[arrayList.size()];
 //integer2 = arrayList.toArray();
```

### 3,栈的操作

```
Stack<Integer> stack = new Stack<Integer>();//堆栈的定义
```

* 两个栈操作的范例

```java
//两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。
public class Solution {
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();
    
    public void push(int node) {
        stack1.push(node);
        
    }
    
    public int pop() {
        while(!stack1.isEmpty()){
            stack2.push(stack1.pop());
        }
        int res=stack2.pop();
        while(!stack2.isEmpty()){
            stack1.push(stack2.pop());
        }
        return res;
    }
}
```

```java
import java.util.*;

public class StackTest {
    /**
     * @param args
     */
    public static void main(String[] args) {
        Stack stack = new Stack(); // 创建堆栈对象 
        System.out.println("11111, absdder, 29999.3 三个元素入栈"); 
        stack.push(new Integer(11111)); //向 栈中 压入整数 11111
        printStack(stack);  //显示栈中的所有元素
 
 
        stack.push("absdder"); //向 栈中 压入
        printStack(stack);  //显示栈中的所有元素
 
        stack.push(new Double(29999.3)); //向 栈中 压入
        printStack(stack);  //显示栈中的所有元素
 
        String s = new String("absdder");
        System.out.println("元素absdder在堆栈的位置"+stack.search(s));      
        System.out.println("元素11111在堆栈的位置"+stack.search(11111));
 
        System.out.println("11111, absdder, 29999.3 三个元素出栈"); //弹出 栈顶元素 
        System.out.println("元素"+stack.pop()+"出栈");
        printStack(stack);  //显示栈中的所有元素
        System.out.println("元素"+stack.pop()+"出栈");
        printStack(stack);  //显示栈中的所有元素
        System.out.println("元素"+stack.pop()+"出栈");
        printStack(stack);  //显示栈中的所有元素
    }
 
    private static void printStack(Stack<Integer> stack ){
        if (stack.empty())
            System.out.println("堆栈是空的，没有元素");
            else {
                System.out.print("堆栈中的元素：");
                Enumeration items = stack.elements(); // 得到 stack 中的枚举对象 
                while (items.hasMoreElements()) //显示枚举（stack ） 中的所有元素
                    System.out.print(items.nextElement()+" ");
            }
        System.out.println(); //换行
    }
    
    //使用for循环的方式遍历栈是很方便的（第二种方法）
    private static void printStack2(Stack<Object> stack ){
        if (stack.empty())
            System.out.println("堆栈是空的，没有元素");
            else {
                System.out.print("堆栈中的元素：");
                for(Object o: stack){
                <span style="white-space:pre">	</span> System.out.print(o+" ");
                }
        System.out.println(); //换行
       }
    }
}
/*
运行结果
11111, absdder, 29999.3 三个元素入栈

堆栈中的元素：11111

堆栈中的元素：11111 absdder 

堆栈中的元素：11111 absdder 29999.3 

元素absdder在堆栈的位置2

元素11111在堆栈的位置3

11111, absdder, 29999.3 三个元素出栈

元素29999.3出栈

堆栈中的元素：11111 absdder 

元素absdder出栈

堆栈中的元素：11111 

元素11111出栈

堆栈是空的，没有元素   */
```

### 3,数二进制中1的个数

* 两种方法

```java
//>>>代表逻辑右移，int占4个字节共32位，因此移位32次
public int 1NumberOf1(int n) {
		int count = 0;
        for(int i = 0; i < 32; i++){
            if((n >>> i & 1) == 1)
                ++count;
        }
        return count;
    }
//二进制数循环减一，并与自身相与，记录直到n为0相减的次数即为1的个数
public int 2NumberOf1(int n) {
        int count = 0;
        if(n == 0)
            return count;
		while(n != 0){
         	++count;
            n = (n-1) & n;
        }
        return count;
    }
```

### 4,数组中奇偶数的处理

>  输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

```java
 public void reOrderArray(int [] array) {
         int j = 0;//定位需要确定位
	        for(int i = 0;i<array.length;i++){
	            if(array[i]%2==1){
	            	//如果是奇数的话
	            	if(i!=j){
	            		int temp = array[i];
	            		int k = i;
	            		for(k = i;k>j;k--){
	            			array[k]=array[k-1];//遇到一个奇数，依次将其移动到偶数前面
	            		}
	            		array[k]=temp;//把奇数的值填入
	            		
	            	}
	            	
						j++;
					
	            }
	        }
    }
```

### 5,输出链表节点

> 输入一个链表，输出该链表中倒数第k个结点
>
> `思路`
>
> 代码思路如下：两个指针，先让第一个指针和第二个指针都指向头结点，然后再让第一个指正走(k-1)步，到达第k个节点。然后两个指针同时往后移动，当第一个结点到达末尾的时候，第二个结点所在位置就是倒数第k个节点了  

```java
public ListNode FindKthToTail(ListNode head,int k) {
        if(head==null||k<=0){
            return null;
        }
        ListNode pre=head;
        ListNode last=head;
        for(int i=1;i<k;i++){//例如倒数第二个，pre和last索引相差1
            if(pre.next!=null){
                pre=pre.next;
            }
            else {return null;}
        }
        while(pre.next!=null){
            pre=pre.next;
            last=last.next;
        }
        return last;
    }
```

### 6,反向链表

> 输入一个链表，反转链表后，输出新链表的表头
>
> `思路1`
>
> 链表的反转 等价于反转链表的指针，只要把原链表中的指针反转，便是链表的反转
>
> /*
> 当middle指针指向的节点不为空时，我们需要用after来保存它下一个节点，防止链表断开后，无法继续后移。middle的next指向pre实现反序，然后middle和pre同时后移一步即可，此时middle指向下一个待考察的节点，直到middle指向空为止，说明链表已完成反序操作。
> */

```java
public ListNode ReverseList(ListNode head) {
        //pre始终指向已反序的最后一个节点
        ListNode pre = null;
        //middle始终指向正在考察节点
        ListNode middle = head;
        //after始终指向待反序的第一个节点，也就是middle之后
        ListNode after = null;
        while(middle != null) {
            //更新after
            after = middle.next;
            //对考察的节点进行反序
            middle.next = pre;
            //更新pre
            pre = middle;
            //后移middle, 换下一个待考察节点
            middle = after;
        }
        //因为pre始终指向已反序的最后的一个节点
        return pre;
    }

```

> `思路2`
>
> 还是上面的想法，只不过我们这次充分利用head来代替middle作用，我们赋予head新的语义，使其始终指向已完成反序的最后一个节点

```java
    /**
     * 充分利用head指针和外加2个辅助指针
     
     */
    public static ListNode ReverseList2(ListNode head) {
        ListNode pre = null;
        ListNode after = null;
        while(head != null) {
            after = head.next;
            head.next = pre;
            pre = head;
            head = after;
        }
        return pre;
    }

```

> `思路3`
>
> 我们使其先走到链表的末尾，确保每次回溯时都返回最后一个节点的指针。同时从倒数第二个结点开始反序。
> head.next.next = head; 是指使当前节点的下一个节点指向自己
> head.next = null; 断开与下一个节点的联系，完成真正的反序操作

```java
    /**
     * 牛逼的递归实现
     */
    public static ListNode ReverseList3(ListNode head) {
        if(head == null || head.next == null) {
            return head;
        }
        ListNode reverseHead = ReverseList3(head.next);
        head.next.next = head;
        head.next = null;
        return reverseHead;
    }

```

[参考出处](<https://blog.csdn.net/dawn_after_dark/article/details/80765535>)

> `另外一个简单的理解`
>
> 思路：
> 链表的反转 等价于反转链表的指针，只要把原链表中的指针反转，便是链表的反转
> 比如 原链表中 head指向head.next，先把head.next保存起来（不然改变head的指向后，原链表会断开，找不到下一个节点），然后改变head指向result（新建节点），再用result表示新链表的表头
> 1>2>3>4
>
> 1(result) 2>3>4
>
> 1<2(result) 3>4
>
> 1<2<3(result) 4
>
> 1<2<3<4(result) 