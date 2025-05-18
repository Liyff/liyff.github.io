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

};

A1 a;	//实例化a的大小是8

**没有成员变量的类大小是1**，为什么是1，不是0，？1不是为了存储数据，是为了占位表示这个实例存在。

class A2

{

};



##### **this指针**

//this是谁调这个成员函数，这个this就指向谁，

class Date

{

​	private:

​				int _year;

​				int _month;

​				int _day;

​	public:

​				void 	Init(int	year,	int	month,	int	day)		//	void 	Init(Date*	this,	int	year,	int	month,	int	day)

​				{

​						_year = year;	// this-> _year = year;

​						_month = month;	//this-> _month = month;

​						_day = day;	//this-> _day = day;

​				}

​				void	Print()

​				{

​						cout << _year << "-" << _month << "-" << _day << endl;

​				}	

};





**this指针是存在栈上的，因为它是一个形参**



#### 2.构造函数

默认构造函数

自定义构造函数

全缺省构造函数

```
class Date
{

private:

	int _year;
	int _month;
	int _day;

public:
	//构造函数，在对象构造时调用的函数
	//如果我们没有显式定义构造函数，C++编译器会自动生成一个无参构造函数
	
	//无参构造语法坑：1.针对内置类型成员变量没有做处理 
	// 2.针对自定义类型成员变量，调用它的构造函数初始化
	Date(int year,int month,int day)
	{
		_year = year;
		_month = month;
		_day = day;
	}
	Date()//一旦用户显式定义有参构造函数，编译器就不会自动生成无参构造
	{

	}

	//更好的方式——》全缺省
	/*
	Date(int year = 0, int month = 1, int day = 1)
	{
		_year = year;
		_month = month;
		_day = day;

	}
	*/



};
```



#### 3.析构函数

未显式定义，编译器自动生成，在对象生命周期结束后自动调用。**完成对象里面的资源清理工作**

```
class Stack{

public:
 Stack(int n = 10)
 {
	_a = (int*)malloc(sizeof(int) * n);
	_size = 0;
	_capacity = 0; 
 } 
 ~Stack()
 {
	free(_a);
	_size = _capacity = 0;
 }
 
};
```



#### 4.拷贝构造



```
Date(int year = 0, int month = 1, int day = 1)
{
	_year = year;
	_month = month;
	_day = day;

}
Date(Date& d)
{
	_year = d._year;
	_month = d._month;
	_day = d._day;
	
}


int main()
{
	Date d1(2025,5,12);
	Date d2(d1);//调用拷贝构造
	Date d3 = d1;



	return 0;
}
```

![image-20250518222605610](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250518222605610.png)

#### 5.运算符的重载

bool operator==(Date& d);

bool operator>(Date& d);

```
	
bool operator==(Date& d) //d1.operator(&d1,d)
{
	return _year == d._year &&
		_month == d._month &&
		_day == d._day;
}

bool operator>(Date& d)
{
	if (_year > d._year)
	{
		return true;
	}
	else if (_year == d._year && _month > d._month)
	{
		return true;
	}
	else if (_year == d._year && _month == d._month && _day > d._day)
	{
		return true;
	}
	return false;

}
	
int main()
{
	Date d1(2025,5,12);
	Date d2(2025,5,12);
	d1 == d2;	//d1.operator==(d2);

	return 0;
}
```

