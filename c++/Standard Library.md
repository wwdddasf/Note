### 1.math.h

```c++
result = sqrt(argument);	//计算算数平方根
result = pow(argument, exponent);	//计算n次方
```

### 2.stdlib.h

```c++
result = rand()	//随机数
    
```

### 3.limits.h

```
CHAR_BIT
CHAR_MAX
CHAR_MIN
..._MAX
..._MIN
```

### 4.string.h

```c++
result = strlen();	//判断字符串长度(char),'\0'终止
string str;			//str可以复制&加法运算 例如 str1 = str2;
					//					str3 = str1 + str2;
strcat(str1, str2); //str2 to str1
strcpy(str1, str2); //str2 to str1
.length()			//Determine the length of a string
.size()				//Determine the length of a string
.at(i) 				//Output the i-th character of the string
str[i] = '';		//Modify the i-th character
.at(i) = '';		//Modify the i-th character
.insert(pos,data)	//Insert starting
.erase(pos,counts)	//Delete starting from position
.substr(starting position,lasting position)
```

string

```c++
array.size();		//判断字符长度(char)
getline(cin, array);			//获取字符串
```

### 5.fstream

```c++
ofstream ofs;					 //创建对象
ofs.open("文件路径", 打开文件方式)		//打开文件
ofs << "写入的数据"; 			  //写数据
ofs.close();					 //关闭文件
```

打开文件方式

```c++
ios::in					//为读文件而打开文件
ios::out				//为写文件而打开文件
ios::ate				//初始位置：文件尾
ios::app				//如果文件存在先删除，再创建
ios::binary				//二进制方式
```

### 6.ctype.h

```c++
isalpha(ch);			//是字母retrun非零值
ispunct(ch);			//是符号return非零值
isdight();				//数字
isspace();				//空白
isalnum();				//字母数字
iscntrl();				//控制符
isgraph();				//除空格外
islower();				//小写字母
isprint();				//打印字符包括空格
isupper();				//大写字母
isxdight();				//十六进制数字
tolower();				//大写字符return小写
toupper();				//小写字符return大写
```

### 7.Vector Container

```c++
vector<int>v1;
vector<int>v2(v1.begin(), v2.end());
vector<int>v3(counts, element);
vector<int>v4(v3);
v2 = v1;				// Assignment
.assign(starting position, last position)	//Assignment左闭右开
.push_back(element);		// Tail insert element
.pop_back();				// Remove the last element
.insert(starting position, element)
.insert(starting position, counts, element)
.erase(position)
.erase(starting position, ending position)
.clear();

.begin()
.end()
.empty()				// Empty when true else false
.capacity()				// Determine capacity
.resize(size)			// resize   Default to filling with 0
.resize(size, element)	// Change the fill value
    
.front()				// Return the first element
.back()					// Return the last element
    
.swap(v)				// swap
vector<int>(v).swap(v);	// Use swap to reduce memory
.reserve(size)			// Reserved space
```

### 8.Deque Container

```c++
// Assigment
d2 = d1;
d3.assign(d1,begin(),d1.end());
d4.assign(10, 100);
// size
d.empty();
d.size();			// No capacity interface
d.resize(number);
d.resize(number,element);
//insert element
d.insert(d.begin(), element);
d.insert(d.beigin(),count, element);
d.insert(d.begin(), d2.begin(), d2.end());	//Insert the sencond constainer into this container
d.push_back(element);
d.push_front(element);
d.pop_back(element);
d.pop_front(element);
d.erase(position);
d.erase(starting position, ending position);
d.clear();
//print function
void printDeque(const deque<int>&d) {
	for (deque<int>::const_iterator it = d.begin(); it != d.end(); it++) {
		cout << *it << " ";
	}
	cout << endl;
}

sort(starting position, ending position);		// sort

```

### 9.Stack Container

```c++
s.push();		// Push onto stack
s.pop();		// Pop from stack

s.size();		// Stack size
s.top();		// Top of the stack

s.empty();		// Determine if it is empty
```

### 10.Queue Container

~~~c++
q.push(p);	// join the queue
q.pop(p);	// Dequeue
q.front();
q.back();
q.empty();
q.size();
~~~

### 11. List Container

~~~c++
// Assigment
L2 = L1;
L3.assign(L2.begin(), L2.end());
L4.assign(10, 100);
// Size
L1.swap(L2);
L1.empty();
L1.size();
L1.resize();

L.push_back();
L.push_front();
L.pop_back();
L.pop_front();
L.insert(position, element);
L.erase(position);
L.remove(element);			// Remove all occurrences of the element from the linked list
L.clear();

L.front();  //The use of [] and at interfaces is not allowed
L.back();
	
L.reverse();
L.sort();	//Algorithm sort is not supported;only the member function sort is supported

bool myCompare(int v1, int v2){
    return v1 > v2;
}
L.sort(myCompare)		//Sort in reverse order
~~~

### 12.Set Container

```c++
s1.insert();
s1.empty();
s1.size();
s1.swap();
						//set automatic sorting
.insert(element);
.clear();
.erase(position);
.erase(begin,end);
.erase(element);

.find(key);
.count(key);

multiset
    
pair<type,type>p( , );
pair<type,type>p2 = make_pair( , );
//Sort according to the functor rules
class MyCompare{
public:
    bool operator()(int v1, int v2){
        return v1 > v2;
    }
}
set<int,MyCompare>s;		

class Person{
public:
    Person(string name, int age){
        this->m_Name = name;
        this->m_Age = age;
    }
    string m_Name;
    int m_Age;
}
class ComparePerson{
public:
    bool operator()(const Person&p1,const Person&p2){
        return p1.m_Age > p2.m_Age;
    }
}
set<Person,comparePerson>s;
```

### 13.map

```c++
map<type,type>m;
m.insert(pair<type,type>(1,10));

.size();
.empty();
.swap(st);

.insert(element);
m.inset(pair<int,int>(1,10));
m.insert(make_pair(2,20));
m.insert(map<int,int>::value_type(3,30));
m[4] = 40;

.clear();
.erase();

map<int,int>::iterator pos = m.find(3);
int num = m.count(3);

class MyCompare{
    public:
    bool operator()(int v1, int v2){
		return v1 > v2;
    }
};
for(map<int,int,MyConpare>::iterator it =;;)
```

### 14.Algorithm

~~~c++
for_each(v.begin(),v.end(),function);
for_each(v.begin(),v.end(),functor());

tansform(v.begin(),v.end(),vTarget.begin(),Transform());

vector<int>::iterator it = find(v.begin(),v.end(),5);
vector<int>::iterator it = find_if(v.begin(),v.end(),GreaterFive());
vector<int>::iterator pos = adjacent_find(v.begin(),v.end());//查找相邻重复元素return adjacent element
bool ret = binary_search(v.begin(),v.end(),element);//必须为有序序列 Must be an ordered sequence
int num = count(v.begin(),v.end(),40);
int num = count_if(v.begin(),v.end(),Greater20());

sort(v.begin(),v.end());
sort(v.begin(),v.end(),greater<int>());//Sort in descending order

random_shuffle(v.begin(),v.end());
srand((unsigned int)time(NULL));

merge(v1.begin(),v1.end(),v2.begin(),v2.end(),vTarget.begin());//将两个有序序列排序给vTarget    Sort the two ordered sequences into vTarget
vTarget.resize(v1.size() + v2.size());

reverse(v.begin(),v.end());

copy(v1.begin(),v1.end(),v2.begin());
v2.resize(v1.size());

replace(v.begin(),v.end(),20,2000); //Replace 20 with 2000
replace_if(v.begin(),v.end(),Greater30(),3000);

swap(v1,v2);

vector<int>::iterator itEnd = set_intersection(v1.begin(),v1.end(),v2.begin(),v2.end(),vTarget.begin());  //计算交集  Calculate the intersection
for_each(vTarget,begin(),itEnd(),myPrint);
vTarget.resize(min(v1.size(),v2.size()));

vector<int>::iterator itEnd = set_union(v1.begin(),v1.end(),v2.begin(),v2.end(),vTarget.begin()); //计算并集
for_each(vTarget.begin(),itEnd,myPrint);

vector<int>::iterator itEnd = set_difference(v1.begin(),v1.end(),v2.begin(),v2.end(),vTarget.begin());
for_each(vTarget.begin(),itEnd(),myPrint)  //计算差集
v.Target.resize(max(v1.size(),v2.size()));

max();
min();
~~~

### 15.numeric

```c++
int total = accumulate(v.begin(),v.end(),0);    // 0 as the starting cumulative value
fill(v.begin(),v.end(),value);
gcd(,);


```

### 16.String Container

~~~c++
int position = str.find();
str.substr(0,position);
stoi();                  // Convert string to integer
~~~







