---
tags:
  - "#linux"
---
## tee
**Command:**`tee [options] file [输出重定向]`
**Options:**
- -a 追加写入
- -i 忽略中断（Ctrl+c）
**Example:**
``` bash
echo "hello world" | tee file1 file2
# Output:
# hello world
# 将内容写入给定文件中（覆盖），同时输出到标准输出

echo "hello world" | tee -a file1 file2 > /dev/null
# 追加写入，且不会输出

sudo echo "export PATH=..." >> /etc/profile
# Permission denied
echo "export PATH-..." | sudo tee /etc/profile
# Successfully!
# 第一个重定向命令没有root权限，所以失败
```

## ps
**Options:**
- `-e | -A` Seclet all progress including daemon progress 
- `-f` 给出每一列的详细信息

## lsof
1. 列出所有打开的文件：`lsof`
2. 查看占用的所有进程并列出进程名：`lsof -c <进程名>`
3. 查看所有建立的socks链接：`lsof -i`
4. 查看某个文件被哪些进程占用：`lsof <文件>`
5. 查看占用某个端口的进程：`lsof -i :<端口号>`

## source or .
直接在当前shell中执行脚本，而不会创建子进程
```shell
source .bashrc
. cnb # cd ~/path/to/nb/
```
如上，当我在 `.bashrc` 中添加了新的环境变量时，在当前shell中并不会生效（因为`.bashrc` 只在shell刚建立时执行一遍），因此我想在当前shell中重新执行一遍 `.bashrc`，使新的环境变量生效，在当前shell中执行，就要使用 `source .bashrc` 或 `. .bashrc`。

另一个例子，我想自动化一个很长的 `cd` 命令，于是我写了一个脚本（只包含一行cd命令），当我直接执行时，其实是在新建立的子shell中执行的，执行完命令该子shell立即退出，对我当前的shell没有任何影响。那么则需要在当前shell中执行该脚本，于是就要使用 `source` 或 `.` 命令。


## dpkg
- `dpkg -l` 列出已安装的包


## wget
用于下载互联网上的资源：`wget [options] url`
- `-O <name>` 指定下载后的文件名
- `-v`verbose, 详细模式，显示下载进度
- `-r` recursive, 递归的下载目录
- `-l` level, 指定递归深度
- `-m | --mirror` 镜像整个网站, 即载整个网站的内容
- `-k | --converts-links` 用于转换文件中的链接，避免下载后的本地文件中，链接依然指向原网站
- `-np | --no-parent` 防止上升到父目录
- 


## kill
`kill <pid>` 结束指定进程


## source exec
执行脚本有3中方式：普通执行，`source`执行和`exec`执行。
1. 普通执行：`./prc`，新建子shell进程，在子进程中执行脚本，执行完成后销毁子进程，返回到父进程
2. `source`执行：`source ./prc`或`. ./prc`，直接在当前shell中执行脚本，不会创建子进程
3. `exec`：使用脚本指定的shell(`#!/bin/sh`等等)替换当前shell，然后再到替换后的shell中执行脚本

## test
`test 1 -eq 2`相当于`[ 1 -eq 2 ]`

## 表达式命令
```
str=`cat file`
# 或者
str=$(cat file)
```
上述语句都是将命令作为一个表达式，捕获命令的返回值作为表达式的值。


## shift
将参数列表看作队列，每执行一次`shfit`，队首元素都将出队（即删除一个参数）。

`shift n` 其中，`n`为数字，表示将队首前`n`个参数出队。

## cut
对文件进行剪裁，并返回剪裁到的内容。输入为文件，但可以利用管道符接受其他输入。
- `-d` 指定分隔符，即在分隔符处剪裁
- `-f` 对剪裁后的序列，指定仅获取索引值为`f`的部分，`one-based index`。
- `-b`表示字节（byte），后面接要提取的字节范围。
- `-c`表示字符（character），与-b类似，但处理多字节字符时更准确。
- `-s` 表示只输出含有分隔符的行，用于忽略不包含分隔符的行。
- `--complement` 返回指定范围之外的所有序列，即反选。
```bash
cut file -b 1,3 # 提取每行第一个和第三个字节
cut file -b 1-3 # 提取每行第一到第三个字节
```

>[!note]
>- cut 处理文件是以行为单元进行处理
>- cut默认不剪裁，即将输入作为一个整体返回。
>- 指定分隔符后，在分隔符处剪裁，生成序列。
>- cut必须指定一种“寻址方式”，`-b -c -f`选择其一，根据寻址方式返回指定范围内的序列
>

> 范围表示：
>`N`     N'th byte, character or field, counted from 1
  `N-`    from N'th byte, character or field, to end of line
  `N-M`   from N'th to M'th (included) byte, character or field                                              `-M`    from first to M'th (included) byte, character or field


## sed
### 一、基本概述

* **名称**：sed（Stream EDitor）
* **作用**：用于对文本进行转换和处理，如查找、替换、删除、插入等。
* **特点**：一行行将文件读入模式空间，处理完后再**将模式空间的内容输出一遍**。一次处理一行的设计模式使得`sed`性能很高，特别是在处理大文件时。

### 二、基本语法

```bash
sed [option]... 'script;script;...' input_file
```

* **option**：可选参数，用于指定`sed`的行为。
* **script**：要执行的脚本，包含一系列的`sed`命令，用于定义对文本的处理方式。
* **input_file**：要处理的输入文件，可以指定多个文件，也可以使用管道从其他命令获取输入。

### 三、常用选项

* **-n**：静默模式，不输出模式空间中的内容到标准输出，常与`p`命令结合使用以打印特定行。
* **-i**：直接修改文件内容，而不是输出到标准输出。使用时需小心，因为这会改变原文件。
* **-e**：指定要执行的多个脚本。
* **-f**：从文件中读取脚本。
* **-r**：使用扩展正则表达式，使脚本中的正则表达式更加简洁。

### 四、地址和命令
sed脚本由地址和命令组成。
* **地址**：用于指定`sed`命令作用的行。可以是行号、行范围或正则表达式。
* **命令**：用于定义对指定行执行的操作如`p`（打印）、`d`（删除）、`s`（替换）等。

### 五、常用命令

* **p**：打印当前模式空间中的内容。
* **d**：删除模式空间中的行。
* **s**：替换文本，格式为`s/pattern/replacement/flags`，其中`pattern`是要匹配的模式，`replacement`是替换后的文本，`flags`是修饰符（如`g`表示全局替换）。
* **a**：在指定行后追加新行，格式为`a\text`，其中`text`是要追加的文本。
* **i**：在指定行前插入新行，格式为`i\text`，其中`text`是要插入的文本。

### 六、示例

1. **替换文本中的字符串**：
   ```bash
   sed 's/old/new/g' file.txt
   ```
   将文件`file.txt`中所有的`old`替换为`new`。地址默认是整个文件，`s`为替换命令，`/old`为命令的第一个参数，是一个正则表达式，`/new/`是命令的第二个参数，是替换后的字符串，`g`是命令选项，表示将所有匹配的字符串都替换掉。

2. **删除匹配到的行**：
   ```bash
   sed '/pattern/d' file.txt
   ```
   删除文件`file.txt`中所有包含`pattern`的行。地址为`/pattern/`，命令为`d`，表示删除。

3. **在指定行后插入新行**：
   ```bash
   sed '2a\New Line' file.txt
   ```
   在文件`file.txt`的第2行后插入一行新文本`New Line`。地址为`2`，命令为`a`，表示在指定行后追加行，`\New Line`表示要添加的内容。

4. **打印指定范围内的行**：
   ```bash
   sed -n '2,4p' file.txt
   ```
   打印文件`file.txt`的第2到第4行。`2,4`为地址，表示第2到第4行，是一个范围，`p`表示打印命令
>[!note]
>sed 将内容输入到模式空间，在模式空间中进行处理，最后将处理完成的内容输出。除了最后的一遍输出，`p`命令在中途也可以输出。取消最后的输出可以使用`-n`选项。

