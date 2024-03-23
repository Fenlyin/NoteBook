### 构造函数
``` cpp
string s1("123456"); 
string s2("123456", pos, count); //截取从pos开始的count个字符组成的子串
string s3("12345", count); //上述pos == 0 时的情况
string s4(n, element); 
string s5(s1, pos); //对s1截取从pos到最后，[pos:]
```

### 成员函数
#### 访问元素
``` cpp
string s1 = "123456";
// 通过索引
s1[2];
// 通过at
s1.at(2);
// 通过迭代器访问
auot = s1.begin();
cout << *it << endl;
```
#### 容量
``` cpp
size(); length(); // 返回元素个数
max_size(); // 返回string容器最大能容纳的元素个数，一般为常量
capacity(); // 返回当前容器的容量，一般情况，capacity > size
```

#### 增加元素
``` cpp
push_back(char ch) // 在末尾添加一个元素
insert(pos, 'c'); // 插入元素
insert(pos, "hello"); // 插入c_string类型的多个元素
insert(pos, string("hello")); // 插入sring类型的多个元素
```

##### 替换
``` cpp
replace(index, count, str);
replace(index, count, n, element);
rep;ace(_first, _last, str);
```
### string to number
``` c++
std::stoi(s); // string to int
std::stol(s); // strint to long
std::stoll(s);// string to long long 

std::stof(s); // float
std::stod(s); // double
std::stold(s);// long double

std::stoi(str, pos, base) //base指定了str代表的数为几进制
```

### number to string
``` c++
int a = 100;
double b = 3.1415926;
cout << std::to_string(a) << endl
	<< std::to_string(b) << endl;
// 100
// 3.14593
```
