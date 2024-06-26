---
tags:
  - "#linux"
---

### 修改系统编码
##### 涉及命令
- `locale`  查看当前编码
- `locale -a` 列出所有字符集
##### 具体修改
1. `sudo vim /etc/profile`
2. `export LANG='zh_CN.UTF-8'`在文件结尾追加
3. `reboot` 重启系统
### 修改启动界面
> 启动界面原理：每次启动或者远程连接，都会执行自动化任务，这个任务会输出文件内容，而文件里面，就是我们看到的界面内容。因此，我们只需要修改相关文件的内容，即可修改启动界面。
- 涉及到的文件(Ubuntu): `/etc/update-motd.d/`目录底下的文件，启动后会执行该目录下的所有可执行文件(shell脚本)
- 涉及到的命令：`run-parts` 将给定目录里的所有文件当作shell脚本去执行
### 修改终端光标样式
``` 
echo -e "\e[1 q"    # 块状闪动
echo -e "\e[2 q"    # 块状不动
echo -e "\e[3 q"    # 下划线闪动
echo -e "\e[4 q"    # 下划线不动
echo -e "\e[5 q"    # 竖线闪动
echo -e "\e[6 q"    # 竖线不动
```
### 修改时区
>修改方法有很多，感觉好乱啊，照着网上的修改了一下，没有全改过来，导致crontab出问题，我无语了，下面这个目前似乎好用：？

`timedatectl`
- `timedatectl list-timezones` 显示可用时区
- `timedatectl set-timezone <Asia/Shanghai>` 设置时区
### 特权端口
在类Unix系统中，小于等于1024的端口被称为特权端口（privileged ports），只有root用户才可以绑定。