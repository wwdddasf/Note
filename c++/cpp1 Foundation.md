### 1.关键字

#### 1.sizeof

```c++
sizeof(number)//判断占用内存空间(字节)
```

#### 2.cout

```c++
cout << hex;//十六进制 	修改cout的输出类型
cout << dec;//十进制
cout << oct;//八进制
cout.setf(ios_base::fixed, ios_base::floatfield);//保留小数点后0
cout << '$' //老版本输出ASCII
```

##### 1.cout.put

```c++
cout.put(argument);	//输出一个字符
cout.put('$')		//输出字符
```

##### 2.wcout



####  3.char

```c++
signed char
unsigned char
```

##### 1.wchar_t

```
```

#### 4.cin

##### 1.wcin

```
```

##### 2.cin.getline

```c++
cin.getline(array, string_length);	//输入字符型 换行后停止输入
```

##### 3.cin.get

```c++
cin.get(array, string_length);		//输入字符型 换行后停止输入
```



#### 5.static

##### 1.static_cast

```c++
result = static_cast<type>(agrument)	//强制转换数据类型
```

#### 6.auto

```c++
auto argument = count;	//自动申明数据类型
```







### 2.函数

```c++
#include<iostream>;
using namespace std;
#include "swap.h"

void swap(int a, int b) {
	int temp = a;
	a = b;
	b = temp;
	cout << "a = " << a << endl;
	cout << "b = " << b << endl;
}//函数的分写(源文件)
```

### 3.指针

```c++
int* p;	 		//定义指针
p = &a;

int* p = NULL;//空指针
int * const p2 = &a;//指针常量
const int * p2 = &a;//常量指针
int* p = arr;//数组arr[0]的指针
```

#### 1.指针函数

```
void swap(int* a,int* b){
	
}
int main(){
	swap(&a, &b)
}
```

### 4.排序

#### 1.冒泡排序

```c++
void bubbleSort(int* arr, int len) {
	for (int i = 0; i < len - 1; i++) {
		for (int j = 0; j < len - i - 1; j++) {
			if (arr[j] > arr[j + 1]) {
				int temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
			}
		}
	}
}
```

### 5.结构体

```c++
struct Student{
	string name;
	int age;
}s1;			//s1 struct可以省略

int main{
	struct Student s1;
	struct Student s1 = {
	...
	}
}
```

#### 1.结构体数组

```c++
struct Student{
	string name;
	int age;
    int score;
}

int main(){
	struct Student stuArray[3]{
		{"张三", 18, 100},
		{"李四", 28, 99},
		{"王五", 38, 66}
	};
	for (int i = 0; i < 3; i++) {
		cout << stuArray[i].name << endl;
        cout << stuArray[i].age << endl;
        cout << stuArray[i].score << endl;
	}
}
```

#### 2.结构体指针

```c++
#include<iostream>
using namespace std;
#include<string.h>

struct student {
	string name;
	int age;
	int score;
};

int main() {
	
	struct student s = { "张三", 43, 12 };
	struct student* p = &s;
	cout << "姓名" << p->name << endl;

	return 0;
}
```

#### 3.结构体嵌套

```c++
struct student1 {
	string name;
	int age;
	int score;
};
struct teacher {
	int id;
	string name;
	int age;
	struct student1 stu;
};

int main() {
	
	struct teacher t;
	t.name = "老王";
	t.age = 40;
	t.id = 11222;
	t.stu.name = "小王";
	
	return 0;
}
```

#### 4.结构体做函数参数

做函数参数，值转递不改变全参，地址传递改变全参

```c++
struct student {
	string name;
	int age;
	int score;
};

void printStudent(struct student s) {
	s.age = 100;
	cout << "子函数中 姓名 年龄 考试分数：" << s.name << s.age << s.score << endl;
}
void printStudent1(struct student* p) {
	p->age = 100;
	cout << "子函数中 姓名 年龄 考试分数：" << p->name << p->age << p->score << endl;
}

int main() {

	struct student s;
	s.name = "张三";
	s.age = 20;
	s.score = 85;

	printStudent(s);
	cout << "main函数1中打印的结果" << s.name << s.age << 		s.score;

	printStudent(s);
	cout << "main函数2中打印的结果" << s.name << s.age << 		s.score;

	return 0;
}
```

#### 5.结构体中const

```c++
void prinstudent(const student* s){	//const 防止误操作修改下行情况
	s->age = 150;  //会修改全局变量
	cout << "姓名" << s->name << ....
}

int main(){
	
	student stu ={"张三", 18};
	printfStudent(&stu);
}
```

### 6.初始化

```
int a = 10;
int a(10);
int a = { 10 };
int a{ 10 };
int a[2]{10,20};
```
