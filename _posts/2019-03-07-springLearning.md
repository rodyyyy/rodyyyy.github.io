---
layout: post
author: Chris Rody
title: SpringLearning
---

spring学习的进阶之路

## spring学习之路

##### 1，spring是一个开源框架，是一个分层的javaSE/EE的一站式（full-stack）轻量级框架

* 一站式框架：有EE开发的每一层解决方案
  * WEB层       ：SpringMVC
  * Service层   ：Spring的Bean管理，Spring声明式事务
  * DAO层        ：Spring的Jdbc模板，Spring的ORM模块



##### 2，spring的优点

> 1,方便解耦，简化开发
>
> 2,AOP编程的支持
>
> 3,声明式事务的支持
>
> 4,方便程序的测试
>
> 5,方便继承各种优秀框架
>
> 6,降低Java EE API的使用难度

##### 3，IOC和DI

* 控制反转，将对象的创建权反转给了Spring   
   * DI：依赖注入，前提必须有IOC的环境，Spring管理这个类的时候将类的依赖的属性注入（设置）进来

     * 依赖

       ``` java
       Class A{  
           }
       Class B{
           public void xxx(A a){      
           } 
       }
       ```

     * 继承：is a

       ```java
       Class A{
       }
       Class B extends A{
       }
       
       ```

      * 聚合：has a

##### 4，SpEL

* SpEL:**Spring Expression Language**，Spring的表达式语言
  * 语法：#{SpEL}	

例子如下：

![SpEL](https://github.com/rodyyyy/rodyyyy.github.io/raw/master/images/SpEL.png