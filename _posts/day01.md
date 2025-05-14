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

#### C++是如何支持函数重载？为什么C语言不支持

list.h   list.c  test.c

1.预处理   ->

2.编译       ->

3.汇编       ->

4.链接       ->