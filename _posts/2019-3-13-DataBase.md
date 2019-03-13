---
layout: post
title: dataBase学习记录
author: Chris Rody
---

数据库笔记

##  dataBaseLearning

### 1，简单运用

```java
public class JdbcTest {

	public static void main(String[] args) {
		
		try {
	 Class.forName(Driver);//1,加载驱动
	 Connection con=DriverManager.getConnection(Url, UserName, UserPassword);
	 //2,创建连接
	 String sql="select * from user where id=10";//3,设置sql语句
	 Statement statement=con.createStatement();//4,创建statement
	 //5，设置参数（这里暂时没有）
	 ResultSet resultset=statement.executeQuery(sql);
	 //6，执行查询，得到resultSet
	 //遍历resultSet，输出结果
	 while(resultset.next()) {
	 System.out.println(resultset.getString(1));
	 System.out.println(resultset.getString(2));
	 System.out.println(resultset.getString(3));
			}
		}
     con.close();//7，释放资源

		catch (SQLException e) {
			e.printStackTrace();
			}
		 catch (ClassNotFoundException e) {
			e.printStackTrace();
		}
	}	
}

```

>Driver="com.mysql.cj.jdbc.Driver";   //新的MySQL驱动包，Driver类变化
>Url="jdbc:mysql://localhost:3306/travelsys?serverTimezone=GMT%2B8"
>UserName="root"
>UserPassword="rody123"

* 具体运行如下：

![表](https://github.com/rodyyyy/rodyyyy.github.io/raw/master/images/数据库1.PNG)

![结果](https://github.com/rodyyyy/rodyyyy.github.io/raw/master/images/数据库2.PNG)