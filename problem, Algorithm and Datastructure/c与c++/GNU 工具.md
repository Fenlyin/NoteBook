### gcc编译c++文件

编译c++文件本应使用 `g++` 命令的，但 `gcc` 也不是不可以，使用 `gcc` 命令：
``` shell
gcc -x c++ main.cpp func.cpp -lstdc++ -o main.exe
```
- `-x` 指定源文件为 `c++` 文件
- `-lstdc++` 指定 `c++` 的标准库

