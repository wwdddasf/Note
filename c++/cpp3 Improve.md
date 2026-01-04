### 1.模板

```c++
#include<iostream>
using namespace std;
template<typename T>
void mySwap(T& a, T& b) {
	T temp = a;
	a = b;
	b = temp;
}
void test01() {
	int a = 10;
	int b = 20;
	mySwap<int>(a, b);
	cout << "a = " << a << endl;
	cout << "b = " << b << endl;
}
int main(){
	test01();
	return 0;
}
```

## STL

### 1.容器

#### 1.vector

```c++
#include<iostream>
using namespace std;
#include<vector>		
#include<algorithm>			

void myPrint(int val) {
	cout << val << endl;
}
void test01() {
	vector<int> v;				// 创建vector容器
	v.push_back(10);			// 向vector容器插入数据
	v.push_back(20);
	v.push_back(30);
	v.push_back(40);
    //通过迭代器访问容器中的数据
	vector<int>::iterator itBegin = v.begin();	//指向第一个元素
	vector<int>::iterator itEnd = v.end();		//指向最后元素下一个位置
	// 第一总遍历方式
    while (itBegin != itEnd) {
		cout << *itBegin << endl;
		itBegin++;
	}
	// 第二种遍历方式
	for (vector<int>::iterator it = v.begin(); it != v.end(); it++) {
		cout << *it << endl;
	}
    // 第三种遍历方式 利用STL算法遍历
	for_each(v.begin(), v.end(), myPrint);
}

int main() {
	test01();	
	return 0;
}
```

```c++
#include<iostream>
using namespace std;
#include<vector>
#include<string.h>

class Person {						//创建Class
public:
	Person(string name, int age) {
		this->m_Name = name;
		this->m_Age = age;
		
	}
	string m_Name;
	int m_Age;
};
void test01() {
	vector<Person>v;
	Person p1("aaa", 10);
	Person p2("bbb", 20);
	Person p3("ccc", 30);
	Person p4("ddd", 40);
	Person p5("eee", 50);
	v.push_back(p1);
	v.push_back(p2);
	v.push_back(p3);
	v.push_back(p4);
	v.push_back(p5);

	for (vector<Person>::iterator it = v.begin(); it != v.end(); it++) {
		cout << "姓名： " << (*it).m_Name << "年龄： " << (*it).m_Age << endl;
		cout << "姓名： " << it->m_Name << "年龄： " << it->m_Age << endl;
	}
}
void test02() {
	vector<Person*>v;					//接收地址，指针接收
	Person p1("aaa", 10);
	Person p2("bbb", 20);
	Person p3("ccc", 30);
	Person p4("ddd", 40);
	Person p5("eee", 50);
	v.push_back(&p1);					//传输地址
	v.push_back(&p2);
	v.push_back(&p3);
	v.push_back(&p4);
	v.push_back(&p5);

	for (vector<Person*>::iterator it = v.begin(); it != v.end(); it++) {
		cout << "姓名： " << (*it)->m_Name << "年龄： " << (*it)->m_Age << endl;
	}									//二级指针，两次解引用
}
int main() {
	test01();
	test02();
	return 0;
}
```

```c++
#include<iostream>
using namespace std;
#include<vector>
#include<string.h>

void test01() {
	vector<vector<int>>v;				//嵌套vector迭代器
	vector<int>v1;
	vector<int>v2;
	vector<int>v3;
	vector<int>v4;
	for (int i = 0; i < 4; i++) {		//像内层迭代器插入数据
		v1.push_back(i + 1);
		v2.push_back(i + 2);
		v3.push_back(i + 3);
		v4.push_back(i + 4);
	}
	v.push_back(v1);					//像外层迭代器插入数据
	v.push_back(v2);
	v.push_back(v3);
	v.push_back(v4);
	for (vector<vector<int>>::iterator it = v.begin(); it != v.end(); it++){
		for (vector<int>::iterator vit = (*it).begin(); vit != (*it).end(); vit++) {
			cout << *vit << " ";
		}
		cout << endl;
	}
}

int main() {
	test01();
	return 0;
}
```

#### 2.string

```c++
string();							// 创建一个空的字符串
string(const char* s);				// 使用字符串s init
string(const string& str);			// 使用一个string对象初始化另一个string对象
string(int n, char c);				// 使用n个字符c初始化
```

```c++
string& operator= (const char* s);		//char*类型字符串 赋值给当前的字符串
string& operator= (const string& s);	//把字符串s赋值给当前的字符串
string& operator= (char c);				//字符赋值给当前的字符串
string& assign(const char* s);   		//把字符串s赋值给当前字符串
string& assign(const char* s, int n);   //把字符串s的前n个字符赋值给当前字符串
string& assign(const string& s);		//把字符创s赋值给当前字符串
string& assign(int n, char c);   		//用n个字符c赋值给当前字符串
```

```c++
string& operator+=(const char* str);				// 重载+=操作符
string& operator+=(const char c);					// 重载+=操作符
string& operator+=(const string& str);				// 重载+=操作符
string& append(const char* s);						// 把字符串s连接到当前字符串结尾
string& append(const char* s, int n);				// 把字符串s的前n个字符连接到当前字符串结尾
string& append(const string& s);					// 同operator+=(const string& str)
string& append(const string& s, int pos, int n);	// 字符串s中从pos开始的n个字符连接到字符串结尾
```

```c++
int find(const string& str, int pos = 0) const;			// 查找str第一次出现的位置，从pos开始查找
int find(const char* s, int pos = 0) const;				// 查找s第一次出现的位置，从pos开始查找
int find(const char* s, int pos, int n) const			// 从pos位置查找s的前n个字符第一次位置
int find(const char c, int pos = 0) const;				// 查找字符c第一次出现的位置
			// find从左往右 rfind从右往左
int rfind(const string& str, int pos = npos) const;		// 查找str最后一次位置，从pos开始查找
int rfind(const char* s, int pos = npos) const;			// 查找s最后一次出现位置，从pos开始查找
int rfind(const char* s, int pos, int n) const;			// 从pos查找s的前n个字符最后一次位置
int rfind(const char c, int pos= 0) const;				// 查找字符c最后一次出现位置
string& replace(int pos, int n, const string& str);		// 替换从pos开始n个字符为字符串str
string& replace(int pos, int n, const char* s);			// 替换从pos开始的n个字符为字符串s
```

```c++
int compare(const string& s) const;				// 与字符串s比较
int compare(const char* s) const;				// 与字符串s比较
```

```c++
string& insert(int pos, const char* s);			// 插入字符串
string& insert(int pos, const string& str);		// 插入字符串
string& insert(int pos, int n, char c);			// 在指定位置插入n个字符c
string& erase(int pos, int n = npos);			// 删除从Pos开始的n个字符
```

```c++
vector<T> v;					// 采用模板实现类实现，默认构造函数
vector(v.begin(), v.end());		// 将v[begin(), end())区间中的元素拷贝给本身
vector(n, elem);				// 构造函数将n个elem拷贝给本身
vector(const vector& vec);		// 拷贝构造函数
```

### 3.仿函数 functional

```c++
class MyAdd {
public:
	int operator()(int v1, int v2) {
		return v1 + v2;
	}
};
void test01() {
	MyAdd myAdd;
	cout << myAdd(10, 10) << endl;
}
```

算数仿函数

~~~c++
void test01(){
    negate<int>n;
    cout << n(50) << endl;
}						//negation operation
void test02(){			//addition operation
    plus<int>p;
    cout << p(10,20) << endl;
}
plus,minus,multiplies,divies,modulus,negate
~~~

关系仿函数

~~~c++
equal_to,not_equal_to
greater,greater_equal
less,less_equal

sort(v.begin(),v.end(),greater<int>());

~~~

逻辑仿函数

~~~c++
logical_and,logical_or,logical_not

transform(v.begin(),v.end(),v2.negin(),logical_not<bool>();
~~~

