## 1.命名空间

using namespace std;//C++中的库都在std中

using std::cout;//部分完全展开 （项目常用）

std::cin



## 2.iostream

cin>>a;

std::cout<<a<<‘ ’<<std::endl;



## 3.缺省参数

### 全缺省（传参从左往右依次传参）

void Func1(int a = 1, int b = 2, int c = 3)

{

}

### 半缺省（从右往左连续缺省）

void Func1(int a, int b = 2, int c = 3)

{

}

## 4.函数重载

### 函数名相同 参数不同（类型不同/个数不同/顺序不同）

**返回值没有要求**（单单只有返回值不同，不构成重载）

void Func2(int a, char b, long c)

{

}

//类型不同

void Func2(int a, double b, long c)

{

}

//个数不同

void Func2(int a, char b)

{

}

//顺序不同

void Func2(int a, long b, char c)

{

}

面试问题：

#### 4.1 C++是如何支持函数重载？为什么C语言不支持

list.h   list.c  test.c

**1.预处理   ->**头文件展开，宏展开，去掉注释，

list.i		test.i

**2.编译       ->**检查语法，转为汇编

list.s		test.s

**3.汇编       ->**汇编转为机器码

list.o		test.o

**4.链接       ->**将目标文件链接到一起

![image-20250514231622986](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250514231622986.png)

**C++  listcpp**反汇编

![image-20250514231715760](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250514231715760.png

![image-20250514231805891](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250514231805891.png)

**C	listc**反汇编

![image-20250514231839926](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250514231839926.png)

#### 4.2 extern “c”

#### **要求C和C++程序都能用C++这个（动态库/静态库）**

extern “c” void Func(int a, int b)

{

}

![image-20250515214330162](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250515214330162.png)

## 5.引用（给已有变量起别名）



#### 特性

int a = 10;

//int& ra;	编译报错，没有初始化

int& ra = a; 	//ra是a的引用，a再取了一个名称叫ra，它们共用一块空间，编译器不会产生新空间

int& rr = ra;

int b = 2;

ra = b; 	//这里是b的值赋值给ra，

**1.引用必须在定义时初始化**

**2.一个变量可以有多个引用**

**3.引用一旦引用一个实体，不能再引用其他实体**



#### 常引用

const int a = 0;	//只读

//int& ra = a;	编译报错，权限放大不行

const int& ra = a;

**变量访问的权限可以缩小不能放大**,	**（适用引用和指针之间的赋值）**

int b = 10;

const int& rb = b;	//引用起别名时，权限可以缩小

![image-20250515221334011](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250515221334011.png)

![image-20250515222526545](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250515222526545.png)

（适用引用和指针之间的赋值）

![image-20250515222828453](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250515222828453.png)

#### 1.引用做参数

![image-20250515223836627](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250515223836627.png)

#### 2.引用做返回值		

作用：少创建临时对象，可以提高效率

![image-20250515224655765](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250515224655765.png)

![image-20250515224849131](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250515224849131.png)

不加static，会出问题，出了作用域栈帧销毁后c就不在了，ret还是引用c那块空间，可能是随机值，

![image-20250515230151854](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250515230151854.png)

加了static，变量c的声明周期是直到程序结束都存在，在数据端的静态区，

static int c = a+b 在第一次调用执行后，**第二次调用就不执行了，因为c已经初始化了**。

{

​	static int c = 1;

​	c = a+b;	//这一句每次调用都会执行

}

![image-20250515230706305](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250515230706305.png)

#### 3.指针和引用区别	

**引用** 语法上是起别名，底层 反汇编实现还是利用指针实现的

int& ra = a;

int* p = &a;

**1.引用必须初始化，**指针没有要求   //int& a = b;      int* p;

**2.引用一个实体后，不能再引用其他实体，**指针可以指向多个

**3.sizeof含义不同，引用是引用类型的大小，**指针始终是4个字节（32位）



## 6.内联函数

inline是一种空间换时间，内联函数在调用地方直接展开，适用频繁调用的小函数Swap()

![image-20250515234757376](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250515234757376.png)

inline 替代宏

#define N 10

const int N = 10;

## 7.auto

int a = 1;

auto b = a;	//b的类型是根据a的类型推导的

int& c = a;	//int

cout<< typeid(b).name()<<endl;	//结果是int



auto& d = a;	//int

auto* e = &a;	//int*

auto f = &a;	//int*

注意：

​	**1.auto不能做参数**

​	**2.auto不能直接做为数组**

![image-20250516215115276](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250516215115276.png)

## 8.范围for

for（auto& e: array)	//加引用，e就是数组元素的别名

{

​	e*=2;

}



for（auto e: array)

{

​	cout<< e<<endl;

}

这样写不行，

![image-20250516215652750](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250516215652750.png)



注意：

C++11中把NULL认为是一个0，空指针用nullptr

int* p = nullptr;

![image-20250516220202019](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250516220202019.png)