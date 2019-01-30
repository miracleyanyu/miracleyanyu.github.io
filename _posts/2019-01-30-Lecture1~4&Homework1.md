---
layout:     post
title:      CS 61B: Lecture 1~4 & Homework 1
subtitle:   总结一下这几天学习的知识及作业！
date:       2019-01-30
author:     Yu
header-img: 
catalog: 	 true
tags:
    - CS 61B
    - Java
---

#CS 61B: Lecture 1~4 & Homework 1

一年前Java没好好学，现在要从头开始全部补回来，诶QAQ。

##Lecture 1&2
主要讲了Objects、Class以及String相关的知识。

> Objects: Repository of Data
	
> Class: Type of Objects
	
> Methods: Procedure or function that operates on objects(or classes)

创建一个String Object分为两个步骤：

	String s1;	//Step1: Declare a String variable
	
	S1 = new String();	//Step2: Assign it a value
	
当然更方便的是用一句话来表`String s1 = new String();`。

>3 String Constructors:
>
> * new String();&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;//Empty String
> * "Whatever"
> * new String(s1);&emsp;&emsp;&emsp;&emsp;&emsp;//Make a copy of s1 references
>
>	s1 is called 'variable', and String(s1) is called 'constructor call'. Constructor always has the same name as class.

   **STRINGS ARE IMMUTABLE!** 也就是说String只要被创建出来，它的值永远不会改变。
   
类似的还有StringBuffer和StringBuilder，通常情况下使用StringBuffer，因为比较快并且节省资源～

接下来是Java I/O Classes: Objects in system class for interacting with users.

>System.out&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;PrintStream
>
>System.in&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;InputStream

ReadLine method is defined on BufferReader objects.

>InputStream&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;Read Raw Dara
>
>InputStreamReader&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;Compose into characters

	BufferedReader keyboard = new BufferedReader(new InputStreamReader(System.in));
	System.out.println(keyboard.readline());

##Lecture 3
创建了Human Class。

	Class Human {
		public int age; 		//primitive
		public String name;	    //references
		
		public void Introduce() {
			System.out.println("My name is " + name);
		}
		
		public void Copy(Human original) {
			age = original.age;
			name = original.name;
		}
		
		public Human(String givenName) {
			age = 12;
			name = givenName;
		}
	}

其中，`public Human(String givenName) {
			age = 12;
			name = givenName;
		}`称为Constructor，Constructor's name is same as Class。
一般情况下，Java都有Default Constructor。

The 'This' Keyword:
	 
	 public void change(int age) {
	 	This.age = age;
	 }
> 'This.age': Human'sage&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;'age': parametters
> 
> (And we can not change the value of 'age'.)

The 'Statis' Keyword:
> Static field:
> 
> * a single variable shared by a whole class of objects
> * also called "class variable"
> 
> > System.out is a static field
> > 
> > main() is always static
> > 
> > In a static method, there is no this

	public static int numberofHuman;
	
	public Human() {
		numberofHuman++;
	}

Lifetimes of variables:
> * A local method is gone when method ends.
> * Instances variable lasts as long as object exists.
> * Class variable(static field) lasts as long as program runs.

##Lecture 4
介绍了一些Primitive Types和If、Switch语句。比较简单就不写啦。

##Homework 1
###Problem 1
输入网址名，倒序返回网站的前四行代码。

首先使用BufferedReader读取键盘输入的网站名，然后创建一个URL，在使用BufferedReader读取网站的代码。输出的话创建五个String，分别存放前五次读取到的内容，然后反着Print就好啦～

	class OpenCommercial {

		public static void main(String[] arg) throws Exception {
   			BufferedReader keyboard;
   			String inputLine;

    		keyboard = new BufferedReader(new InputStreamReader(System.in));

    		System.out.print("Please enter the name of a company (without spaces): ");
    		System.out.flush();        /* Make sure the line is printed immediately. */
    		inputLine = keyboard.readLine();

    		URL point3acres = new URL("https://www."+inputLine+".com");
    		BufferedReader in = new BufferedReader(new 			InputStreamReader(point3acres.openStream()));

    		String firstLine = new String();
    		firstLine = in.readLine();
    		String secondLine = new String();
    		secondLine = in.readLine();
    		String thirdLine = new String();
    		thirdLine = in.readLine();
    		String forthLine = new String();
    		forthLine = in.readLine();
    		String fifthLine = new String();
    		fifthLine = in.readLine();
    
   	 		System.out.println(fifthLine);
    		System.out.println(forthLine);
    		System.out.println(thirdLine);
    		System.out.println(secondLine);
    		System.out.println(firstLine);
    	}
    }
结果如下：
![Problem 1](https://ws1.sinaimg.cn/large/006tNc79ly1fzokrghai5j31400p0tfk.jpg)

###Problem 2
输入一个字符串，删掉第二个字符然后输出。

首先也是使用BufferedReader读取输入的字符串放到String里，然后通过new StringBuffer(inputLine)转为StringBuffer，再使用deleteCharAt()方法就好啦。

	public class Nuke2 {
		public static void main(String[] args) throws IOException {
			BufferedReader keyboard = new BufferedReader(new InputStreamReader(System.in));
			String inputLine;
		
			inputLine = keyboard.readLine();
		
			StringBuffer outputLine = new StringBuffer(inputLine);
		
			System.out.println(outputLine.deleteCharAt(1));
		}
	}
结果如下：
![Problem 2](https://ws4.sinaimg.cn/large/006tNc79ly1fzokyr4zbkj31400p0afd.jpg)

决定以后每一个Homework总结一下，继续学习去了～