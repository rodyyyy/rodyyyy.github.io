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

> Class类封装一个对象和接口运行时的状态，当装载类时，Class类型的对象自动创建
>
> Class.forName：返回与给定的字符串名称相关联类或接口的Class对象。
>
> Class.forName是一个静态方法，同样可以用来加载类。该方法有两种形式：
>
> Class.forName(String name, boolean initialize, ClassLoader loader)和 Class.forName(String className)。第一种形式的参数 name表示的是类的全名；initialize表示是否初始化类；loader表示加载时使用的类加载器。第二种形式则相当于设置了参数 initialize的值为 true，loader的值为当前类的类加载器。