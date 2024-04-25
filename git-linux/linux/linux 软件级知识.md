---
tags:
  - "#linux"
---

## linux用户管理

 	linux用户管理主要设计到两个文件：1. /etc/passwd 2. /etc/group。其中，paaswd存储的是用户相关的信息，一行存储一个用户，每行有7个字段。group存储的是组信息，一行一组，每行四个字段。

- **passwd**: fenlyin:x\:1000:1000:main user:/home/fenlyin:/bin/bash
- 分别为：用户名:用户密码(加密过):用户id:组id:用户描述:用户根目录:用户所用的终端
- **group**：adm:x\:4:syslog
- 分别为：组名:组密码\:组id:组中附属用户列表（一般组密码都为空）
- 两个快捷命令：
  - getent passwd == cat /etc/passwd
  - getent group == cat /etc/group

一个用户只能有一个主组，但能加入多个附属组，组信息中也会显示该组中的附属用户(主组不是该组的用户)。



### **用户方面**

  ##### useradd options username(root)

     - options:
       - -c 指定用户描述
       - -d 指定用户根目录， 但不会创建此目录，所以如果目录不存在，则还要-m创建
       - -m 创建用户目录(此选项没有参数)
       - -g 指定用户组
       - -G 指定用户附属组列表，可以指定多项，eg. -G root, adm
       - -a 增加用户的附属组到附属组列表中，必须与-G一起出现，-aG
       - -s 指定用户终端
       - -u 指定用户id，如果不给出，默认是从上一个用户id递增

  ##### usermod options username(root)

     - 常用选项与 useradd一致，可以为用户指定新的资源值

  ##### userdel options username(root)

     - options：
       - -r 连同用户的根目录一起删除

  ##### 用户密码管理: passwd \[optinons] username

     用户刚创建后没有密码，此时会被系统锁定，无法使用，必须要为其设置密码

     - options:
       - -l 锁定，即禁用账号
       - -u 解锁
       - -d 指定用户的密码为空密码
       - -f 强迫用户下次登陆时修改密码
     - passwd username 修改用户密码
     - 普通用户只能修改自己的密码，且修改前要输入旧密码，超级用户可以修改任意用户密码，其无需旧密码确认。

  5. sudo 命令

     - 要执行sudo命令，用户必须要在sudoer文件中才有权限，而文件中指出，在sudo用户组中的用户拥有权限，因此，用户需要加入sudo用户组中才有权限执行sudo命令。
     - -u username 以指定用户的身份执行命令，不加此选项默认是以root身份执行命令。

  6. id, groups

     - 查看用户信息

#### 用户组方面

  1. groupadd options groupname (root)
     - -g 指定组id，与-o协同使用表示可以与已有的其他组id相同
  2.  groupdel groupname (root)
     - 删除组
  3. groupmod options groupname(root)
     - -g -o 与groupadd一致
     - -n 指定新组名
  4. newgrp groupname
     - 切换当前用户到指定的组中，已使用指定组的权限，前提是当前用户已经是指定组的成员(主成员或附属成员都可)
  
	

### screen简单理解

##### 新建虚拟终端
  - screen \[-S|-R name]
  - 不指定终端名，系统会使用linux默认的命名方法，会很麻烦。
  - -R 选项，如果name终端已经存在，则直接连接，如果是-S的话，则会创建一个同名的新终端

##### 挂起虚拟终端
  - Ctrl+a d
  - Ctrl+a进入特殊命令模式，在按d键登出

##### 连接虚拟终端
  - screen -r -R pid/name
  - -R 选项， 如果终端不存在，则会创建新终端

##### 清除虚拟终端
  - 在虚拟终端中Ctrl+d登出，或者输入exit
-  在主终端中输入：screen -R pid/name -X quit
- screen -ls 列出所有的虚拟终端
- screen高阶命令：

  - 进入特殊命令模式后：
  - 关闭虚拟终端，相当于exit
  - ？显示所有的命令
## crontab简单理解

+ 开启crontab的日志记录

  1. 修改/etc/rsyslog.d/50-default.conf, 去掉cron前面的注释
  2. 重启 `service rsyslog restart`
  3. 查看 **cat /var/log/cron.log**

+ 配置文件：

  1. 用户：**/var/spool/cron/crontabs/username**
  2. crontab：**/etc/crontab**

  - 在用户配置文件中，任务格式：* * * * * CMD
  - 在crontab软件自身配置文件中，任务格式：* * * * * username CMD

+ 编辑用户配置文件

  + crontab -e
  + 也可以使用vim等文本编辑器，但使用crontab可以检查，如果任务格式有错，关闭时会提醒

+ minute hour day month week

## ssh远程连接linux

​       要使用ssh远程连接linux，那么linux上至少需要安装ssh服务端，自身至少要安装ssh客户端。

### 安装ssh服务端

- dpkg -l | grep ssh 查看有无openssh-server
- 如果无，则：sudo apt-get install openssh-server
- 安装后：ps -e | grep ssh, 看到sshd则说明ssh服务已启动
- 如果没启动，则：sudo service ssh start

​       连接方式有两种：1. 基于用户口令的连接。2. 基于密钥对的连接。

### 基于用户口令的连接

​       ssh username@IP address, 之后需要输入该用户的口令（密码）

### 基于密钥对的连接

- 私钥放在客户端，公钥放在服务端，密钥对生成后便是用户无关的了，比如我用用户fenlyin生成的密钥对，公钥传到服务器，私钥发给sam一份，则sam也可以利用该密钥对登录服务器。
- 公钥会添加在服务器用户根目录中`.ssh/authorized_keys`文件中。
- 生成密钥对：`ssh-keygen -t rsa`， -t type: 即使用rsa非对称加密法。
- 将密钥对传到服务器：`ssh-copy-id username@IPaddress`。传密钥时确保服务端开启了基于口令的连接，即**PasswordAuthentication yes**，因为在传公钥时肯定要建立连接，而此时还不能基于密钥连接，所以只能基于口令连接。

### ssh连接细节

- 使用ssh客户端连接远程服务器时，首先会搜索~/.ssh/know_hosts文件中有无该主机，如果有，则进行密钥连接，否则，
进行口令连接（前提是ssh服务端开启了口令连接）
- 据我猜测，known_hosts中应该存有ip地址和主机的映射关系，因为我前后使用同一个ip地址登录了两台主机，当我等第二台主机时，ssh警告说：远程主机不安全。这是因为本地认为该ip地址应该是主机1的，但现在成为主机2了，那么很可能自己
正在被中间劫持攻击，所以ssh拒绝连接。
- 每个用户应将生成的私钥和公钥存好，之后想要远程连接任意服务器，只需将此公钥上传服务器即可，而私钥用于与服务
器的公钥配对，即理想情况下一个用户一生只需用一个密钥对。

### 通过ssh传输文件
`scp [-r] source destination`
### 从服务端下载文件到客户端：
`scp username@IPaddress:file_path  destination_path`
eg.
`scp kali@kali:/home/kali/test  ~`
### 从客户端上传文件到服务端：
`scp file_path  username@IPaddress:destination_path`
eg.
`scp ~/test  kali@kali:/home/kali`
- destination is always directory, if source is directory type, then add -r option.

## 链接文件
linux中链接文件分为软链接（符号链接）和硬链接。
##### 软链接
`ln -s <源文件> <链接文件>`
软链接相当于指针，会有独一的inode号，有储存空间，其中储存的是源文件的相关信息
##### 硬链接
`ln <源文件> <链接文件>`
硬链接相当于引用（别名），与源文件共享同一inode，只有当所有的硬链接和源文件都被删除时，文件才会被真正删除
硬链接不能跨文件系统创建。

## 磁盘管理
挂载了disk就无法再挂载该disk的partition，反之，挂载了partition，也就无法挂载disk
##### mount与umount
- `mount 设备名 挂载点`
- `umount 设备名[挂载点]` 卸载时输入设备名或该设备的挂载点都一样
##### fuser
`fuser -v 挂载点` 查看正在访问该挂载点的进程、用户
`fuser -km 挂载点` 结束所有正在访问该挂载点的进程

##### mkfs
`mkfs.<type> partition` 
`mkfs -t <type> partition`
格式化分区为type类型的文件系统
