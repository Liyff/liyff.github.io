## 面向对象

#### 1.封装

​	把想给你看的数据给你看，不想给你看的数据封装起来。-》访问限定符

class Stack

{

//1.成员变量

//2.成员函数

private:

​			int* _a;

​			int _size;

​			int _capacity;



public:

​			void 	Push(int x);

​			void 	Pop();

​			bool 	Empty();

}

![image-20250516221919360](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250516221919360.png)

##### **类的实例化**

声明和定义区别？？？

声明是一种承诺，承诺要干嘛，但是还没做，定义就是把这个事落地了。



//类里面声明，类外面定义

void Stack::Push(int x)

{

}



Stack s1;	//类实例化对象后，只存储成员变量

**原因是一个类可以实例化出N个对象，每个对象的成员变量都可以存储不同的值，但函数调用的是同一个成员函数。**



内存对齐规则

class A1

{

private:

​			int _a;

​			char _ch;

public:

​			void fun();

}

A1 a;	//实例化a的大小是8

**没有成员变量的类大小是1**，为什么是1，不是0，？1不是为了存储数据，是为了占位表示这个实例存在。

class A2

{

}



##### **this指针**

class Date

{

​	private:

​				int _year;

​				int _month;

​				int _day;

​	public:

​				void 	Init(int	year,	int	month,	int	day)

​				{

​				}

​				void	Print();

}





this指针是存在栈上的，因为它是一个形参