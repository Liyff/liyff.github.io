## stack

stack/queue/priority_queue   容器适配器

std::deque 双端队列



```
 #include<vector>
 #include<list>
 
namespace liyf
 {
    template<class T,class Container>
    class stack
    {
    public:
        stack() {}
        void push(const T& x) {
        	_c.push_back(x);
        }
        void pop() {
        	_c.pop_back();
        }
        T& top() {return _c.back();}
        const T& top()const {return _c.back();}
        size_t size()const {return _c.size();}
        bool empty()const {return _c.empty();}
    private:
        Container _c;
     };
     
     
    template<class T,class Container>
    class queue
    {
    public:
        queue() {}
        void push(const T& x) {
        	_c.push_back(x);
        }
        void pop() {
        	_c.pop_front();
        }
        T& back() {return _c.back();}
        const T& back()const {return _c.back();}
        T& front() {return _c.front();}
        const T& front()const {return _c.front();}
        size_t size()const {return _c.size();}
        bool empty()const {return _c.empty();}
    private:
        Container _c;
    };
 }
 
 
 
 int mian()
 {
 	stack<int,vector<int>> st;
 	queue<int,list<int>> que;  //不能用vector,不支持头插
 	
 	return 0;
 }
```





[ 最小栈](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/)

[逆波兰表达式求值](https://leetcode.cn/problems/8Zf90G/)