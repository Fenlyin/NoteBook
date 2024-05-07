---
tags:
  - "#linux"
---
### tee
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

### ps
**Options:**
- `-e | -A` Seclet all progress including daemon progress 

### lsof
1. 列出所有打开的文件：`lsof`
2. 查看占用的所有进程并列出进程名：`lsof -c <进程名>`
3. 查看所有建立的socks链接：`lsof -i`
4. 查看某个文件被哪些进程占用：`lsof <文件>`
5. 查看占用某个端口的进程：`lsof -i :<端口号>`

### source or .
直接在当前shell中执行脚本，而不会创建子进程
```shell
source .bashrc
. cnb # cd ~/path/to/nb/
```
如上，当我在 `.bashrc` 中添加了新的环境变量时，在当前shell中并不会生效（因为`.bashrc` 只在shell刚建立时执行一遍），因此我想在当前shell中重新执行一遍 `.bashrc`，使新的环境变量生效，在当前shell中执行，就要使用 `source .bashrc` 或 `. .bashrc`。

另一个例子，我想自动化一个很长的 `cd` 命令，于是我写了一个脚本（只包含一行cd命令），当我直接执行时，其实是在新建立的子shell中执行的，执行完命令该子shell立即退出，对我当前的shell没有任何影响。那么则需要在当前shell中执行该脚本，于是就要使用 `source` 或 `.` 命令。