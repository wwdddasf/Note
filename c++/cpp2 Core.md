### 1.内存

代码区

全局区

```c++

static int g_a = 10;//静态变量

const int c_l_a= 10;//const 修饰的常量
```

堆区

```
形参
局部变量
```



栈区



#### new

```c++
int* funcion(){
	int* p = new int(10);
	return p;
}

int main(){
	int* p = function();
}

void test02(){			//new一个数组
    int* arr = new int[10];
    for(int i = 0; i < 10; i++){
        arr[i] = i + 100;
    }
}
```

释放

```c++
delete p;
delete[] arr;//释放数组
```

### 2.引用

```c++
int &b = a;	//必须初始化 	//int &b; 	错误
int& b = 10;//错误 	只能是一个变量	
```

#### 1.引用做函数参数

```c++
void swap(int* a, int* b){
	int temp = a;
	a = b;
	b = temp;
}
int main(){
	swap(a, b);
	return 0;
}						//形参修饰实参
```

#### 2.引用做函数返回类型

```
int& test(){
	int a = 10;
	return a;
}
int main(){
	int &ref = test();
    cout << ref << endl;
    cout << ref << endl;	//error
}						//内存被释放，只能输出一次
```

static int a = 10;

####  3.引用与static

```c++
int& test(){
	static int a = 20;
	return a;
}
int main(){
	int& ref = test();
	test() = 1000;
	cout << ref2 << endl;		//输出1000
}
```

### 3.函数

#### 1.函数的默认参数

```c++
int function(int parameter = 10, int parameter = 20);
int main(){
	cout << funcion(3) << endl;
}				//result = 23	//默认值，后必须为默认值
```

#### 2.函数的站位参数

```c++
void function(int a, int){
	statement;
}
/*
void function(int a, int = 0){
	statement;
}
*/
int main(){
	function(10, 10);
	return 0;
}
```

#### 3.函数的重载

```c++
void function1();
void function(int a);
void function(double a);
void function(int a , double b);
void function(double a, int b);	//均构成重载，返回值不可作为重载
```

#### 4.函数的注意事项

```c++
void function(int& a);
void function(const int& a);
int main(){
	int a = 10;
	function(a);	//调用function(int& a);
	function(10);	//调用function(const int& a);
    return 0;
}
```

### 4.面向对象

#### 1.封装

权限

```
public
protected
private
```

#### 2.对象的初始化和清理

##### 1.构造函数与析构函数与拷贝构造函数

```c++
#include<iostream>
using namespace std;

class Person {
public:
	Person() {
		cout << "Person的构造函数的调用" << endl;
	}
    /*
    ~Person(){
    	cout << "Person的析构函数的调用" << endl;
    }			//调用一次后被释放
    */
};
void test01() {
	Person p;
}
int main() {
	test01();
	return 0;
}				//函数名与类名相同
```

```c++
class Person{
public:
	Person(){
		statement;		//	无参构造函数(默认构造函数)
	}					
	Person(int a){
		statement;		//  有参构造函数
	}
	Person(const Person& p){
		age = p.age;	
	}					//  拷贝构造函数
    ~Person(){
        statement;
    }					//  析构函数
}
int main(){
    Person p1();			//  error，被编译器当成函数
    Person p1;				//  默认构造函数（无参构造函数）
    
    Person p2 = Person(10);	//	显示法
    Person p3 = Person(p2);	//	显示法   拷贝构造函数
    
    Person(10)；			   //   初始化匿名对象，先析构后输出
    Person(p3); 			//	不要初始化拷贝构造匿名函数
    
    Person p4 = 10;			//	隐式转换法
    Person p5 = p4;			//	隐式转换法 拷贝构造函数
}
```

```c++
#include<iostream>
using namespace std;

class Person {
public:
	Person() {
		cout << "Person 构造函数的调用" << endl;
	}
	Person(int a) {
		cout << "Person 有参构造函数的调用" << endl;
	}
	~Person() {
		cout << "Person 析构函数的调用" << endl;
	}
	Person(const Person& p) {
		m_age = p.m_age;
		cout << "Person 拷贝构造函数的调用" << endl;
	}
	int m_age;
};

void test01() {
	Person p1(10);
	Person p2(p1);
}

void doWork(Person p) {

}
void test02() {
	Person p;				// 拷贝出一个副本
	doWork(p);				// 调用默认构造函数&拷贝构造函数
}

Person doWork2() {
	Person p1;				// 返回值为Person
	return p1;				// 拷贝出新的一个对象p1，地址不同
}
void test03() {
	Person p = doWork2();
}
int main() {

	test03();

	return 0;
}
```

##### 2.深拷贝与浅拷贝

```c++
#include<iostream>
using namespace std;

class Person {
public:
	Person() {
		cout << "Person 构造函数的调用" << endl;
	}
	Person(int age, int height) {
		m_Age = age;
		m_Height = new int(height);		//申请内存
		cout << "Person 有参构造函数的调用" << endl;
	}
	~Person() {
		if (m_Height != NULL) {		
			delete m_Height;		// 删除内存
			m_Height = NULL;		// 将指针置空
		}
		cout << "Person 析构函数的调用" << endl;
	}
	Person(const Person& p) {
		m_Age = p.m_Age;
		cout << "Person 拷贝构造函数的调用" << endl;
		m_Height = new int(*p.m_Height);  //为指针创造一块新的内存，防止浅拷贝，重复删除
	}
	int m_Age;
	int* m_Height;
};

void test() {
	Person p1(18, 160);
	cout << "p1的年龄和身高为：" << p1.m_Age << *p1.m_Height << endl;		
	Person p2(18, 160);
	cout << "p2的年龄和身高为：" << p2.m_Age << *p2.m_Height << endl;

}

int main() {
	test();
	return 0;
}
```

##### 3.初始化列表

```c++
Person(int a, int b,int c):m_A(a),m_B(b),m_C(c){

}
```

##### 4.调用顺序

```c++
#include<iostream>
using namespace std;
#include<string.h>

class Phone {
public:
	Phone(string pName) {
		m_PName = pName;
	}
	string m_PName;
};

class Person {
public:
	Person(string name, string pName) : m_Name(name), m_Phone(pName) {

	}
	string m_Name;
	string m_Phone;
};

int main() {

	return 0;
}
```

##### 5.静态成员

###### 1.静态成员变量

```c++
#include<iostream>
using namespace std;

class Person {
public:
	static int m_A;			//静态成员变量
};
void test01() {
	Person p;
	cout << p.m_A << endl;	//result:100
	Person p2;
	p2.m_A = 200;
	cout << p2.m_A << endl; //result:200
	cout << p.m_A << endl;	//result:200
}
int Person::m_A = 100;		//指定Person类里的m_A
int main() {

	test01();

	return 0;
}
```

###### 2.静态成员函数

```c++
public:
	static void function(){
	
	}
	
int main(){
	Person::function();
}						//静态成员函数只能调用静态成员变量
```

仅有非静态成员变量在对象上

##### 6.this指针

```c++
#include<iostream>
using namespace std;

class Person {
public:
	Person(int age) {
		this->age = age;
	}
	Person& PersonAddAge(Person& p) {	//返回值为引用
		this->age += p.age;
		return *this;					//返回地址
	}
	int age;
};

int main() {
    
	Person p1 = 10;						//赋值
	Person p2 = 10;
	p1.PersonAddAge(p2).PersonAddAge(p2); //累加
	cout << p1.age << p2.age << endl;

	return 0;
}
```

##### 7.const

```c++
void showPerson() const {		//常函数用const修饰
	this->a = 100;				//修改变量
}							
mutable int a;					//特殊变量，在常函数中可以修改

void test(){
    const Person p;			  	//常对象
}								//常对象只能调用常函数
```

#### 3.友元

```c++
#include<iostream>
using namespace std;
#include<string.h>

class Building {
	friend void goodGay(Building* building);	//让goodGay函数访问private权限
public:
	Building() {
		m_SittingRoom = "客厅";
		m_BedRoom = "卧室";
	}
public:
	string m_SittingRoom;
private:
	string m_BedRoom;
};
void goodGay(Building* building) {
	cout << "好基友的全局函数 正在访问： " << building->m_SittingRoom << endl;
	cout << "好基友的全局函数 正在访问： " << building->m_BedRoom << endl;
}
void test01() {
	Building building;
	goodGay(&building);
}
int main() {
	test01();
	return 0;
}
```

#### 4.运算符重载

可以发生函数的重载

##### 1.加法运算符

```c++
#include<iostream>
using namespace std;
#include<string.h>

class Person {
public:
	Person operator+(Person& p) {			//成员函数重载
		Person temp;
		temp.m_A = this->m_A + p.m_A;
		temp.m_B = this->m_B + p.m_B;
		return temp;
	}
	int m_A;
	int m_B;
};
Person operator+(Person& p1, Person& p2) {	//全局函数重载
	Person temp;
	temp.m_A = p1.m_A + p2.m_A;
	temp.m_B = p1.m_B + p2.m_B;
	return temp;
}
Person operator+(Person& p1, int numb){		//class&int
    Person temp;
	temp.m_A = p1.m_A + numb;
	temp.m_B = p1.m_B + numb;
	return temp;
}
void test01() {
	Person p1;
	p1.m_A = 10;
	p1.m_B = 10;
	Person p2;
	p2.m_A = 10;
	p2.m_B = 10;
	//Person p3 = p1.operator+(p1, p2);
	//Person p3 = p1 + p2;
	cout << "p3.m_A" << p3.m_A << endl;
	cout << "p3.m_B" << p3.m_B << endl;

}

int main() {

	test01();

	return 0;
}
```

##### 2.左移运算符

```c++
class Person{
	friend ostream& operator<<(ostream&, Person& p);
public:
	Person(int a,int b){
	m_A = a;
	m_B = b;
	}
private:
	int m_A;
	int m_B;
}
ostream& operator<<(ostream&, Person& p){
	out << "m_A = " << p.m_A << "m_B = " << p.m_B;
	return out;
}
void test01(){
	Person p(10,10);
	cout << p << "hello world" << endl;
}
```

##### 3.递增运算符

```
```

#### 5.继承

```c++
class Person : Person public{

}
```

查看继承信息cmd

```c++
cl /d1 reportSingleClassLayout类名 文件名
```

虚继承

```c++
class Sheep :virtual public Animal{};
```

#### 6.多肽

纯虚函数

```
public:
	virtual void function() = 0;
```

#### 7. 读写文件

写

```c++
#include<iostream>
using namespace std;
#include<fstream>
void test01() {
	ofstream ofs;
	ofs.open("test.txt", ios::out);
	ofs << "姓名：张三" << endl;
	ofs << "性别：男" << endl;
	ofs << "年龄：18" << endl;
	ofs.close();
}
int main() {
	test01();
	return 0;
}
```

读

```c++
#include<iostream>
using namespace std;
#include<fstream>
#include<string>

void test01() {
	ifstream ifs;
	ifs.open("test.txt", ios::in);
	if (!ifs.is_open()) {
		cout << "文件打开失败" << endl;
		return;
	}

	//char buf[1024] = { 0 };
	//while (ifs >> buf) {
	//	cout << buf << endl;
	//}

	//char buf[1024] = { 0 };
	//while (ifs.getline(buf, sizeof(buf))) {
	//	cout << buf << endl;
	//}

	//string buf;
	//while (getline(ifs, buf)) {
	//	cout << buf << endl;
	//}

	char c;
	while ((c = ifs.get()) != EOF) {
		cout << c;
	}
	ifs.close();
}
int main() {
	test01();
	return 0;
}

```

