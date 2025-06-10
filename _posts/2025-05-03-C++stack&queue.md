## stack

stack/queue/priority_queue   **容器适配器** 都不支持迭代器遍历，因为他们都包含特殊性质FILO,FIFO

std::deque 双端队列



```
 #include<vector>
 #include<list>
 
namespace liyf
 {
    template<class T,class Container>
    //template<class T,class Container=deque<T> >
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
    //template<class T,class Container=deque<T> >
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



双端队列

```
缺点：
1.大量频繁operator[]的效率低。
2.迭代器遍历相对复杂，效率也有一些影响
```

[最小栈](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/)

[逆波兰表达式求值](https://leetcode.cn/problems/8Zf90G/)



优先级队列

```
ptiotity_queue


namespace liyf
{
	
	template<class T, class Container = vector<T>, class Compare = less<T>>
	//默认大根堆
	class priority_queue
	{
	public:
		void AdjustUp(int child)
		{
			Compare com;
			int parent = (child-1)/2;
            
            while(child>0)
            {
            	//if(com(_con[parent]，_con[child]))
            	if(_con[child]>_con[parent])
            	{
            		swap(_con[child],_con[parent]);
            		child =parent;
            		parent = (child-1)/2;
            	}
            	else
            	{
            		break;
            	}
            }
		}
		
		void AdjustDown(int root)
		{
			int parent = root;
			int child = 2*parent+1;
			Compare com;
			while(child<_con.size())
			{
			
				//if(child+1 < _con.size() && com(_con[child+1]，_con[child]) )
                if(child+1 < _con.size() && _con[child]<_con[child+1])
                {
                    child++;
                }
				
				//if(com(_con[child],_con[parent]))
                if(_con[parent]<_con[child])
                {
                    swap(_con[parent],_con[child]);
                    parent = child;
                    child = parent*2+1;
                }
                else
                {
                    break;
                }
			
			}
		}
		
		
		void push(const T& x)
		{
			_con.push_back(x);
			AdjustUp(_con.size()-1);
		}
		
		void pop()
		{
			swap(_con[0],_con[_con.size()-1]);
            _con.pop_back();
            
            AdjustDown(_con[0]);
		}
		
		T& top();
		size_t size()
		{
			return _con.size();
		}
		
		
		bool empty()
		{
			return _con.empty();
		}
	
	private:
		Container _con;
	}
	
	//struct和class只有默认访问权限不一样，一个私有，一个公有
	//一般情况，成员部分私有，部分公有，就用class
	//所有成员都开放或共有，就用struct
	
	//仿函数	它的对象可以像函数一样去使用
	template<class T>
	struct less
	{
		bool operator()(const T& x1,const T& x2)
		{
			return x1<x2;
		}
	};
	template<class T>
	struct greater
	{
		bool operator()(const T& x1,const T& x2)
		{
			return x1>x2;
		}
	};
	
	
	
}


int main()
{
	//priority_queue<int> pq;
	priority_queue<int,vector<int>,greater<int>> pq;
	pq.push(1);
	pq.push(2);
	pq.push(3);
	pq.push(4);
	
	
	liyf::less<int> lessFunc;
	cout << lessFunc(1,2) << endl;
	
	//升序 less <
	sort(v.begin(),v.end());
	
	//降序  greater >
	sort(v.begin(),v.end(),greater<int>());
}
```





[076. 数组中的第 K 个最大元素](https://leetcode.cn/problems/xx4gT2/)