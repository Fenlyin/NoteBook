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
