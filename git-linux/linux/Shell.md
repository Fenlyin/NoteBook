### 运行Shell脚本的方法
1. `./test.sh` 这种方法告诉系统，运行当前目录下的test.sh文件，不会去PATH中搜索，如果使用这种方式，test.sh文件开头要指定解释此文件的解释器，否则无法运行
2. `/bin/bash test.sh` 作为解释参数器参数运行，此时脚本开头无需指定解释器
- `#!/bin/bash` 指定解释器的语法

### Shell 变量
##### 定义变量
shell脚本中定义变量和给变量重新赋值时，等号两边最好不要有空格。
``` bash
x=1    # 在shell中养成这种习惯
x = 1  # 最好不要使用这种风格
```
##### 使用变量
- `echo $x` 如果没有$符号，将直接输出"x"
- `echo ${varName}` 使用"{}"符号指定变量名的边界
##### 只读变量
``` bash
str1="hello"
readonly str1
# 使用readonly关键字声明变量的只读属性
# 如果先readonly再初始化，这是不行的，因为已经readonly了
```
##### 删除变量
- `unset x` 使用unset关键字
- 只读变量不能被删除
##### 变量类型
shell作为一门动态编程语言，其变量类型会根据变量的值或字面值进行推导，但在Shell中，字面值只有一种，字符型，如此一来，声明整型变量就要用到其他方法了。
- `declare -i x=1`| `typeset x=1` 使用这两种方法声明整型变量
##### 特殊变量
- 环境变量：操作系统级的变量，由操作系统或用户设置，用于配置Shell行为和其执行环境
- 参数变量：$0 表示脚本名称，$1, $2...等表示脚本参数，\$#表示参数数量，\$?表示上一个命令的退出状态

### 字符串
##### 拼接字符串
将各个子串一次罗列出来即可，中间千万不能以空格分隔，要紧贴
``` bash
str1="world"
str="hello"" "$str1
# Output: hello world
# 也可：
str=hello" "$str1
```
##### 字符串长度
``` bash
str=hello
echo ${#str}    # 不知道什么原理，记住吧
# Output: 5
```
##### 字符串截取
``` bash
str="hello world"
echo ${str:6:5}    # 从索引6开始截取5个字符
# Output: world
```
##### 字符串查找
``` bash
str="hello world"
echo `expr index "$str" h`
# Output: 1
echo `expr index "$str" lo`
# Output: 3
# 待查字符串必须要以引号包围的形式出现，后面是待查字符。找出字符串中第一次出现待查字符的位置即可，索引从1开始！！！
```
### Shell数组
##### 定义及访问
``` bash
# shell中的数组，分为index型和associatex型（字典）

# index:
arr1=(1 2 3 4)    # 元素间以空格分隔
echo ${arr1[0]}   # 访问
a=${arr1[0]}
b=${arr1[1]}
c=$a+$b
echo $c    # Output: 3  index型数组中数字的字面值又是整型，可能是例外吧，真是搞不懂

# associate:（也就是字典）
declare -A arr2
arr2["name"]="John"
arr2[age]=12
arr2[name]=John
# 因为Shell中字面值只有字符型，因此"name" 和 name 都可

# “@”一次访问所有元素
echo ${arr[@]}    # 遍历并输出所有元素
```
##### 数组的长度
``` bash
length=${#arr[@]} 
# 或
length=${#arr[*]}    # 取得数组长度

length=${#arr[1]}    # 取得元素长度
```

### 输入输出重定向
重定向都是针对于命令，一个命令只要有输入或输出，那么就可以重定向。默认情况下，一个命令有一个输入源：`stdin`文件描述符：`0`；两个输出，分别是标准输出：`stdout`文件描述符：`1`；标准错误输出：`stderr`文件描述符：`2`
- `cat file > file1`或`cat file >> file1` 输出重定向到file1，`>` 表示覆盖写入，`>>`表示追加写入
- `wc -l < file` 输入重定向
``` 
$ wc -l << EOF
> Hello
> World
> !
> EOF
$ 3
# 注意：结束符EOF必须要顶格且后面不能有任何字符
```
- `cat file >> file1 2>&1` 将stdout和stderr合并输出到file1中
##### /dev/null 文件
此文件是一个特殊文件，写入到此的内容会被自动丢弃，而且也无法读出有效内容，因此，如果想要屏蔽某命令的输出，可以将输出重定向到此文件。