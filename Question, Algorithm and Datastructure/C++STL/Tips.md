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

### 容器的迭代器
- 前向迭代器  只支持`operator++`
- 双向迭代器  支持`operator++` 和 `operator--`
- 随机访问迭代器 支持双向迭代器的操作，且支持 `operator-` 和 `operator+`;