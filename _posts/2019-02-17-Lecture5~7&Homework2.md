---
layout:     post
title:      CS61B:Lecture 5~7&Homework 2
subtitle:   总结一下所学的内容和作业
date:       2019-02-17
author:     Yu
header-img: 
catalog: true
tags:
    - CS 61B
    - Java
---

# CS 61B: Lecture 5~7 & Homework 2

年快过完了，学习学习学习！

## Lecture 5&6
这两部分Lecture主要讲了各种loop，和array的概念。

**"While" loop:**

	public static boolean isPrime(int n) {
		int divisor = 2;
		while(divisor < n) {
			if(n % divisor == 0) {
				return false;
			}
			divisor++;
		}
		return true;
	}

**"For" loop:**

	public static boolean isPrime(int n) {
		for(int divisor = 2; divisor < n; divisor++) {
			if(n % divisor ==0) {
				return false;
			}
		}
		return true;
	}
	
**"Do" loop:**

> Always execute at least once.
> 
> 可以avoid一些repeated code(method and call)

	do {
		s = keyboard.readline();
		process(s);
	} while(s.length > 0)

 还有continue和break语句，continue只能在循环中出现，目的是跳到本次循环的最后，进行下一次循环，break则是直接退出循环。
 
**ARRAYS: An object consisting of a numbered list of variables.
        Each is a primitive type or reference.**
<br>Automatic array construction:<br>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;int[][] table = new int[x][y];&emsp;&emsp;&emsp;&emsp;//x arrays of y ints
<br>Initializers:<br>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;Human[] b = {kayla, Sam, Bob};
<br><br> String[] args: List of command-line arguments

	char[] c;    //reference to array(any length)
	c = new char(4);
	c[0] = 'b';  //default: ASCII 0

**Sieve of Evatosthenes:**

	public static void printPrime(int n) {
		boolean[] prime = new boolean[n+1];
		int i;
		for(i = 2; i <= n; i++) {
			prime[i] = true;
		}
		for(int divisor = 2; divisor * divisor < n; divisor++) {
			if(prime[divisor]) {
				for(i = 2 * divisor; i <= n; i = i + divisor) {
					prime[i] = false;
				}
			}
		}
		for(i = 2; i <= n; i++) {
			if(prime[i])
				System.out.println(" " + i);
		}
	}

Multi-dimensional Arrays:<br>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;Two-dimensional arrays: An array of references to arrays.

**Pascal's Triangle:**<br>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;row i represents coefficients of (x+1)^i

	public static void pascalTriangle(int n) {
		int[][] pt = new int[n][];
		for(int i = 0; i < n; i++) {
			pt[i] = new int[i + 1];
			pt[i][0] = 1;
			for(int j =1; j < i; j++) {
				pt[i][j] = pt[i-1][j-1] + pt[i-1][j];
			}
			pt[i][i] = 1;
		}
		return pt;
	}

最后讲了一下善用Constant:<br>

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;"Final" keyword: value can not be changed.

> Bad:&emsp;&emsp;&emsp;&emsp;if(month == 2) {....}
> 
> Good:&emsp;&emsp;&emsp;&emsp;public final static int FEBRUARY = 2;
> <br>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;if(month == FEBRUARY) {...}

##Lecture 7
主要讲了跟array相对应的另一个概念：list

**List:**
> Store as an array
> <br>&emsp;&emsp;&emsp;&emsp;Disadvantages:
> <br>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;1. Insert item at beginning or end -> time proportional to length of array
> <br>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;2. Arrays have a fixed length

Linked Lists: A recursive data type<br>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;Made up of "nodes": an item and a reference to next node in list.

	public class ListNode {
		int item;
		ListNode next;
	}

	ListNode l1 = new ListNode();
	ListNode l2 = new ListNode();
	l1.next = l2;     //l1.next and l2 points to the same thing.

Node operations:

	public ListNode(int item, ListNode next) {
		this.item = item;
		this.next = next;
	}

> Advantages:
> 
> * Inserting item in the middle of liked list takes constant time
> * can keep growing

Insert:
	
	public void insertAfter(int item) {
		next = new ListNode(item, next);
	}

Insert before: start from the 1st node, find whose next is l2.

> Disadvantages:
> 
> * finding the nth item takes time proportional to n -> length of list

	public ListNode nth(int position) {
		if(position == 1)
			return this;
		else if((position < 1) || (next == null))
			return null;
		else
			return next.nth(position - 1);
	}

List of Objects:
	
	public class SListNode {
		public Object item;
		public SListNode next;
	}
	
	x = new SListNode("soap", x);    //insert
	
	public class SList {
		private SListNode head;
		private int size;
		
		public SList() {
			head = null;
			size = 0;
		}
		.
		.    (insert_
		.
	}    //在insert的时候可以保证所有指向SList的都得到更新

##Homework 2
有关日期的一个小程序。

	package hw2Part1;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Scanner;

	public class hw2Part1 {
		public static void main(String[] args) throws IOException {
			String inputLine;
			BufferedReader keyboard = new BufferedReader(new InputStreamReader(System.in));
			inputLine = keyboard.readLine();
			System.out.println(inputLine);
			hw2Part1 date = new hw2Part1(inputLine);
			System.out.println(date.year);
			//String[] date = inputLine.split("/");
			//System.out.println(date[0]+date[1]+date[2]);
			//System.out.println(Integer.parseInt(date[2]));
			//isLeapYear(Integer.parseInt(date[2]));
			//isValidDate(Integer.parseInt(date[0]), Integer.parseInt(date[1]), Integer.parseInt(date[2]));
			//hw2Part1 date1 = new hw2Part1(2, 1, 2001);
			//hw2Part1 date2 = new hw2Part1(1, 1, 2000);
			//System.out.println(date2.difference(date1));
		}
	
		private int day;
		private int month;
		private int year;
	
		/** Constructs a Date object corresponding to the given string.
		 *  @param s should be a string of the form "month/day/year" where month must
		 *  be one or two digits, day must be one or two digits, and year must be
		 *  between 1 and 4 digits.  If s does not match these requirements or is not
		 *  a valid date, the program halts with an error message of your choice.
		 */
		public hw2Part1(String s) {
			String[] dat = s.split("/");
			if(isValidDate(Integer.parseInt(dat[0]), Integer.parseInt(dat[1]), Integer.parseInt(dat[2]))) {
				this.month = Integer.parseInt(dat[0]);
				this.day = Integer.parseInt(dat[1]);
				this.year = Integer.parseInt(dat[2]);
			}
			else
				System.exit(0);
		}
	
		/** Constructs a date with the given month, day and year. If the date is
		 *  not valid, the entire program will halt with an error message.
		 *  @param month is a month, numbered in the range 1...12.
		 *  @param day is between 1 and the number of days in the given month.
		 *  @param year is the year in question, with no digits omitted.
		 */
		public hw2Part1(int month, int day, int year) {
			if(isValidDate(month, day, year) == false)
				System.exit(0);
			this.month = month;
			this.day = day;
			this.year = year;
		}
	
		/** Returns a string representation of this date in the form month/day/year.
		 *  The month, day, and year are expressed in full as integers; for example,
		 *  12/7/2006 or 3/21/407.
		 *  @return a String representation of this date.
		 */
		 public String dateToString() {
			 return(this.month+"/"+this.day+"/"+this.year);
	 	}
	 
		/** Checks whether the given year is a leap year.
	 	*  @return true if and only if the input year is a leap year.
	 	*/
		public static boolean isLeapYear(int year) {
			  if((year%4 == 0) && (year%100 != 0) || (year%400 ==0))
				  return true;
		  	else 
				  return false;
		}
	
		/** Returns the number of days in a given month.
	 	*  @param month is a month, numbered in the range 1...12.
	 	*  @param year is the year in question, with no digits omitted.
	 	*  @return the number of days in the given month.
	 	*/
		public static int daysInMonth(int month, int year) {
			  int day = 0;
		  	switch(month) {
		  		case 1:
		  			day = 31;
		  			break;
		  		case 2:
		  			if(isLeapYear(year) == true)
		  				day = 29;
		  			else
		  				day = 28;
			  		break;
			  	case 3:
			  		day = 31;
		  			break;
			  	case 4:
			  		day = 30;
			  		break;
		  		case 5:
		  			day = 31;
			  		break;
			  	case 6:
		  			day = 30;
		  			break;
			  	case 7:
			  		day = 31;
		  			break;
			  	case 8:
			  		day = 31;
		  			break;
			  	case 9:
			  		day = 30;
			  		break;
		  		case 10:
			  		day = 31;
			  		break;
			  	case 11:
		  			day = 30;
		  			break;
			  	case 12:
			  		day = 31;
			  		break;
			  }
			  return day;
		}
	
		/** Checks whether the given date is valid.
		 *  @return true if and only if month/day/year constitute a valid date.
		 *
		 *  Years prior to A.D. 1 are NOT valid.
		 */
		public static boolean isValidDate(int month, int day, int year) {
			  if(((month == 1) || (month == 3) || (month == 5) || (month == 7) || (month == 8) || (month == 10) || (month == 12)) && (day <32) && (day > 0)) {
				  System.out.println("The date entered is valid.");
			  	return true;
		  	}
		  	else if(((month == 4) || (month == 6) || (month == 9) || (month == 11)) && (day <32) && (day >0)) {
				  System.out.println("The date entered is valid.");
				  return true;
			  }
		  	else if((isLeapYear(year) == true) && (month == 2) && (day < 30) && (day >0)) {
				  System.out.println("The date entered is valid.");
				  return true;
			  }
			  else if((isLeapYear(year) == false) && (month == 2) && (day < 29) && (day >0)) {
				  System.out.println("The date entered is valid.");
				  return true;
			  }
			  else
				  System.out.println("The date entered is not valid.");
				  return false;
		}
	
		/** Determines whether this Date is before the Date d.
		 *  @return true if and only if this Date is before d.
		 */
		public boolean isBefore(hw2Part1 d) {
			if(this.year < d.year)
				return true;
			else if(this.year == d.year && this.month < d.month)
				return true;
			else if(this.year == d.year && this.month == d.month && this.day < d.day)
				return true;
			else
				return false;
		}
	
		/** Determines whether this Date is after the Date d.
		* @return true if and only if this Date is after d.
		*/
		public boolean isAfter(hw2Part1 d) {
			if(this.year > d.year)
				return true;
			else if(this.year == d.year && this.month > d.month)
				return true;
			else if(this.year == d.year && this.month == d.month && this.day > d.day)
				return true;
			else
				return false;
		}
	
		/** * * *
		Returns the number of this Date in the year.
		@return a number n in the range 1...366, inclusive, such that this Date
		is the nth day of its year.  (366 is used only for December 31 in a leap
		year.)
	 	*/
		public int dayInYear() {
			int total = 0;
			for(int i = 0; i < this.month; i++)
				total += daysInMonth(i, this.year);
			total += this.day;
			return total;
		}
	
		/** Determines the difference in days between d and this Date.  For example,
		 *  if this Date is 12/15/2012 and d is 12/14/2012, the difference is 1.
	 	*  If this Date occurs before d, the result is negative.
	 	*  @return the difference in days between d and this date.
		Hint:  use the online Java API to familiarize yourself with all the methods
	available to you in the String class.
		 */
		public int difference(hw2Part1 d) {
			int remain = 0;
			int total = 0;
			if(this.isAfter(d)) {
				if(this.year != d.year && isLeapYear(d.year))
					remain = 366 - d.dayInYear();
				else if(this.year != d.year && !isLeapYear(d.year))
					remain = 365 - d.dayInYear();
				for(int i = (d.year + 1); i < this.year; i++) {
					if(isLeapYear(i))
						total += 366;
					else
						total += 365;
				}
				if(this.year == d.year)
					total += remain + this.dayInYear() - d.dayInYear();
				else
					total += remain + this.dayInYear();
			}
			else if(this.isBefore(d)) {
				if(this.year != d.year && isLeapYear(this.year))
					remain = 366 - this.dayInYear();
				else if(this.year != d.year && !isLeapYear(this.year))
					remain = 365 - this.dayInYear();
				for(int i = (this.year + 1); i < d.year; i++) {
					if(isLeapYear(i))
						total += 366;
					else
						total += 365;
				}
				if(this.year == d.year)
					total += remain + d.dayInYear() - this.dayInYear();
				else
					total += remain + d.dayInYear();
				total = 0 - total;
			}
			return total;
		}
	}
主要method分别实现了：判断闰年、判断日期是一年中的第几天、判断日期是否有效、将输入的字符串日期转换成数字、判断两个日期哪个在前/在后、判断两个日期之间相差的天数。

头大，写了好久才写出来QAQ
