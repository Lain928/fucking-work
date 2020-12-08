# 一、c++类的相关操作
## 1.构造函数和析构函数是否可以为虚函数？
	答：构造函数不能，析构函数可以
	（1）构造函数：虚函数的调用需要虚函数表指针，而该指针存放在对象的内存空间中；
	若构造函数声明为虚函数，那么由于对象还未创建，还没有内存空间，更没有虚函数表地址用来调用虚函数——构造函数了
	（2）析构函数：
	首先析构函数可以为虚函数，而且当要使用基类指针或引用调用子类时，最好将基类的析构函数声明为虚函数，否则可以存在内存泄露的问题。
	举例说明：
	子类B继承自基类A；A *p = new B; delete p;
	1） 此时，如果类A的析构函数不是虚函数，那么delete p；将会仅仅调用A的析构函数，只释放了B对象中的A部分，而派生出的新的部分未释放掉。
	2） 如果类A的析构函数是虚函数，delete p; 将会先调用B的析构函数，再调用A的析构函数，释放B对象的所有空间。
	补充： B *p = new B; delete p;时也是先调用B的析构函数，再调用A的析构函数。
	
	
# 二、c++模板
## 1.函数模板
	声明：
		template <typename T>
		void test(t a)
		{
			cout << a << endl;
		}
	应用：
		int main()
		{
			int a = 0;
			test(a); //自动调用
			test<int>(a); //显示调用
		}
## 2.类模板
	定义：
		template <class T>
		class Stack { 
		  private: 
			vector<T> elems;     // 元素 
		 
		  public: 
			void push(T const&);  // 入栈
			} 
		};
	声明类函数：
		template <class T>
		void Stack<T>::push (T const& elem) 
		{ 
			// 追加传入元素的副本
			elems.push_back(elem);    
		}
	应用:
		Stack<int> intStack;  // int 类型的栈 
        Stack<string> stringStack;    // string 类型的栈 
	

# 三、STL相关库操作
## 1.vector的赋值相关操作
	(1)不可以直接使用“=”进行赋值，因为未重载”=“操作，应使用vector<elem> b(a);

