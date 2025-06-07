## STL标准模板库

**(standard template library)**

#### STL六大容器

![image-20250527222958633](C:\Users\LIYUFENG\AppData\Roaming\Typora\typora-user-images\image-20250527222958633.png)

#### 1.string

```
// size/clear/resize
 void Teststring1()
 {
    // 注意：string类对象支持直接用cin和cout进行输入和输出
     string s("hello, bit!!!");
     cout << s.size() << endl;
     cout << s.length() << endl;
     cout << s.capacity() << endl;
     cout << s <<endl;
 // 将s中的字符串清空，注意清空时只是将size清0，不改变底层空间的大小
     s.clear();
     cout << s.size() << endl;
     cout << s.capacity() << endl;
     // 将s中有效字符个数增加到10个，多出位置用'a'进行填充
    // “aaaaaaaaaa”
     s.resize(10, 'a');
     cout << s.size() << endl;
     cout << s.capacity() << endl;
     // 将s中有效字符个数增加到15个，多出位置用缺省值'\0'进行填充
    // "aaaaaaaaaa\0\0\0\0\0"
     // 注意此时s中有效字符个数已经增加到15个
    s.resize(15);
     cout << s.size() << endl;
     cout << s.capacity() << endl;
     cout << s << endl;
     // 将s中有效字符个数缩小到5个
    s.resize(5);
     cout << s.size() << endl;
     cout << s.capacity() << endl;
     cout << s << endl;
  }
```

##### 1.四个默认成员函数

- 构造函数
- 析构函数
- 拷贝构造            ==>传统写法，现代写法
- operator=重载  ==>传统写法，现代写法

##### 2.遍历

- 重载[]+下标
- iteator        v.begin()    v.end()
- 范围for(底层还是iteator)       auto 

##### 3.reserve（） 

reserve()修改空间大小，resize(n,char ch) 修改数据个数为n,并把扩充的数据填充位ch

##### 4.insert（）

##### 5.substr()

##### 6.find()  rfind()

分离出URL  协议 域名  资源

https://cplusplus.com/reference/string/string/find/



##### 7.getline()

- getline(cin,str)遇到换行才结束

- cin>>和scanf（）遇到空格或者换行就结束输入

#### 2.string实现

```
//构造函数
//析构函数
//拷贝构造
//operator=


#include "stdio.h"
#include <string.h>

using namespace std;

namespace lyf
{
	class string
	{
	public:
		

		string(const char* str = "")
			:_str(new char[strlen(str) + 1])
		{
			strcpy(_str, str);

		}

		string(const string& s)
			:_str(new char[strlen(s._str)+1])
		{
			strcpy(_str, s._str);
		}#include "stdio.h"
#include <string.h>
#include <stdlib.h>
#include <utility>

using namespace std;

namespace lyf
{
	class string
	{
	public:
		

		string(const char* str = "")
			:_str(new char[strlen(str) + 1])
		{
			strcpy(_str, str);

		}

		/*string(const string& s)
			:_str(new char[strlen(s._str)+1])
		{
			strcpy(_str, s._str);
		}

		string& operator=(const string& s)
		{
			if (this != &s)
			{
				char* pstr = new char[strlen(s._str) + 1];
				strcpy(pstr, s._str);
				delete[] _str;
				_str = pstr;

			}
			return *this;
		}*/

		//现代版写法
		string(const string& s)
		{
			string tmp(s._str);
			swap(_str, tmp._str);
		}

		string& operator=(string& s)
		{
			swap(_str, s._str);
			return *this;
		}



		~string()
		{
			if (_str)
			{
				delete[] _str;
				_str = nullptr;
			}
			
		}



	private:
		char* _str;


	};
}

		string& operator=(const string& s)
		{
			if (this != &s)
			{
				char* pstr = new char[strlen(s._str) + 1];
				strcpy(pstr, s._str);
				delete[] _str;
				_str = pstr;

			}
			return *this;
		}



		~string()
		{
			if (_str)
			{
				delete[] _str;
				_str = nullptr;
			}
			
		}



	private:
		char* _str;


	};
}

//begin()  end()
//istream& operator>>(istream& in,string& s);
//ostream operator<<(ostream& out,string& s);

//string增删改查
void push_back();
void append(char* str);
string& insert(int pos,char ch);
string& insert(int pos,char* str);

string& erase(int pos,int len);

int find();

bool operator<();
bool operator==();
bool operator>();
bool operator<=();
bool operator>=();
bool operator!=();


```




#### 练习

1.仅仅反转字母https://leetcode.cn/problems/reverse-only-letters/description/

2.字符串中的第一个唯一字符https://leetcode.cn/problems/first-unique-character-in-a-string/description/

3.验证回文串https://leetcode.cn/problems/XltzEq/description/

4.字符串相加https://leetcode.cn/problems/add-strings/description/

5.字符串相乘https://leetcode.cn/problems/multiply-strings/description/



**ascII码表**（针对早期计算机需要表示英文）值和字母映射关系

unicode计算机科学领域行业里标准，包括字符集，编码方案

strlen(str)不会计入 ‘\0’

**strcpy(tmp, _str)会把 ‘ \0 ’ 拷贝过去**

strncpy(tmp, _str, n)控制长度，拷贝过去的 _str 是n个长度

strstr()

strcmp(char* str1,char* str2)字符串比较
