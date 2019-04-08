---
layout: post
title: 反射
author: Chris Rody
---

### 反射的简要概念

> 反射：Java 的特征之一，它允许运行中的 Java 程序获取自身的信息，并且可以操作类或对象的内部属性
>
> 核心： JVM 在运行时才动态加载类或调用方法/访问属性，它不需要事先（写代码的时候或编译期）知道运行对象是谁

~~~
通过反射，我们可以在运行时获得程序或程序集中每一个类型的成员和成员的信息。程序中一般的对象的类型都是在编译期就确定下来的，而 Java 反射机制可以动态地创建对象并调用其属性，这样的对象的类型在编译期是未知的。
~~~

> 用途:开发各种通用框架，很多框架（比如 Spring）都是配置化的（比如通过 XML 文件配置 Bean），为了保证框架的通用性，它们可能需要根据配置文件加载不同的对象或类，调用不同的方法，这个时候就必须用到反射，运行时动态加载需要加载的对象。
>
> 注意事项：由于反射会额外消耗一定的系统资源，因此如果不需要动态地创建一个对象，那么就不需要用反射。另外，反射调用方法时可以忽略权限检查，因此可能会破坏封装性而导致安全问题。

```java
Class<?> cls=Class.forName(act[0]);
			    Object oj=cls.newInstance();
//反射生成指定类的实例/*java.lang.class是反射操作的入口，因为reflect的所有类都没有公共构造函数， * 所以为了实例化其中的类，必须调用合适的class*/			 
			    try {
						Method method=cls.getMethod(act[1], HttpServletRequest.class,HttpServletResponse.class);
					try {
						String result=(String) method.invoke(oj, request,response);
                    }
                }
```

