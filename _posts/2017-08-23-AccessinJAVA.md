---
layout: post
title: JAVA中的访问权限释疑
date: 2017-08-26
categories: blog
tags: [Thinking in JAVA]
description: 一段程序释疑访问权限的区别
---

## JAVA访问控制权限

　　对于很多初学者来说，对于JAVA类之前的权限修饰符会感到特别困惑，为什么要有“访问控制权限”这一说？JAVA中Public,Protected,Private以及默认Default权限之间的区别又是什么？

## 权限的目的

　　考虑这样一个场景：当你编写了一个程序类库以提供给客户使用。类库中的某一些方法是直接提供给客户使用的，客户可以根据业务需要直接使用这些方法，我们可以称之为“效用代码”。另外一些方法（称其为辅助代码）则是为这些“效用代码”提供辅助计算的，并不能直接被客户使用，因为客户不需要了解详细的实现过程，客户需要做的只是输入必备的参数，就能够得到他想要的结果。

*为了使得实现过程（辅助代码）与实现方法（效用代码）相分离，在程序设计过程中，就需要用到* **权限控制**。

## 分离的目的

　　将实现过程与实现方法**分离**，即便利客户的使用，还有利于代码的更新与维护。相信大家在使用C语言或者是其他程序中，都会用到Math函数或者是类库来解决很多数学问题，比如：求平方根，求指数的底。在我们的使用过程中，只需要调用Math函数或者是类库，直接使用求平方根函数（方法）,就可以求得所想要的结果。我们不需要深究计算机内部是如何求平方根，只需要知道如何使用该函数（方法）就可以了，而关于具体的实现方法，这是程序开发者需要考虑的事情。为了方便程序的使用以及维护，程序开发者“有意”将实现过程与实现方法分离，将实现过程隐藏起来，只提供实现方法给客户。

## Default Public Protected Private权限

**Public**
　　在中文版的《Thinking in java》中，public被定义为是*接口访问权限*。只要通过合适的import或者放置在同一个包中，其可以被所有的类访问。
**Default**
　　中文版的《Thinking in java》中，Default被定义为*包访问权限*。什么是包访问权限呢？包访问权限就是，该类或者是方法可以被放置在*同一个package*中的类访问，但无法被处于不同包内的类访问。
**Protected**
　　中文版的《Thinking in java》中，Protected被定义为*继承访问权限*。与*包访问权限*不同的是：继承访问权限可以通过继承，来访问到不同包中具有Protected权限的类或方法。
**Private**
　　顾名思义，除自身类之外，任何其他的类都无法访问

## 程序释疑

　　在JAVA中创建一个AccessTest类，放置在名为net.jinhao的包中：
```java
package net.jinhao;
public class AccessTest {
  protected AccessTest(){
	   System.out.println("初始化AccessTest()");//**类的初始化，为Protected权限**//
   }
  protected void saypr() {
	  System.out.println("继承权限Say()");//**saypr()方法，为Protected权限**//
  }
  public void saypb() {
	  System.out.println("公有权限saypb()");//**saypb()方法，为Public权限**//
  }
  private void saypri() {
	  System.out.println("私有saypb()");//**saypri()方法，为Private权限**//
  }
  void saydef() {
	  System.out.println("默认访问saydef()");//**saydef()方法，为包访问权限**//
  }
}

```
在名为net.jinhao的包中新建一个Access类：
```java
package net.jinhao;
public class Access {
  public static void main(String[] args) {
	  AccessTest at = new AccessTest();
	  at.saypb();
	  at.saypr();
	  //at.saypri();无法访问//
	  at.saydef();
  }
}
```
运行Access,输出：
```java
初始化AccessTest()
公有权限saypb()
继承权限Say()
默认访问saydef()
```
　　在本例中，由于Access类与AccessTest()类放置在同一个包中，所以在Access类中可以访问除了具有Private权限的所有方法。
****
　　接下来在名为net.zuojinhao的包中新建一个Access类：
```java 
package net.zuojinhao;
import net.jinhao.*;
public class Access extends AccessTest {
    //AccessTest at = new AccessTest();访问protected初始化方法会报错//
	public static void main(String[] args) //必须通过继承来对AccessTest()初始化//
	{   Access at = new Access();
		at.saypb();
		at.saypr();
		//at.saypri();访问私有报错//
		//at.saydef();即使继承，也无法访问具有默认权限的方法//
	}
	}
```
运行该类，输出：
```java
初始化AccessTest()
公有权限saypb()
继承权限Say()
```
　　由于Access类与AccessTest()类放置在不同中，且AccessTest()具有继承访问权限，如果不通过继承，就无法对AccessTest()进行初始化;并且，由于saypri()和saydef()分别具有Private权限和包访问权限，所以即使继承了AccessTest(),仍然无法访问saypri()和saydef()方法。

