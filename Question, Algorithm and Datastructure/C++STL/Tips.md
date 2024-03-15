### string to number
``` c++
std::stoi(s); // string to int
std::stol(s); // strint to long
std::stoll(s);// string to long long 

std::stof(s); // float
std::stod(s); // double
std::stold(s);// long double
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