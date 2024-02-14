### linux用户管理

 	linux用户管理主要设计到两个文件：1. /etc/passwd 2. /etc/group。其中，paaswd存储的是用户相关的信息，一行存储一个用户，每行有7个字段。group存储的是组信息，一行一组，每行四个字段。

- **passwd**: fenlyin:x\:1000:1000:main user:/home/fenlyin:/bin/bash
- 分别为：用户名:用户密码(加密过):用户id:组id:用户描述:用户根目录:用户所用的终端
- **group**：adm:x\:4:syslog
- 分别为：组名:组密码\:组id:组中附属用户列表（一般组密码都为空）
- 两个快捷命令：
  - getent passwd == cat /etc/passwd
  - getent group == cat /etc/group

一个用户只能有一个主组，但能加入多个附属组，组信息中也会显示该组中的附属用户(主组不是该组的用户)。



##### 主要命令

- **用户方面**

  1. useradd options username(root)

     - options:
       - -c 指定用户描述
       - -d 指定用户根目录， 但不会创建此目录，所以如果目录不存在，则还要-m创建
       - -m 创建用户目录(此选项没有参数)
       - -g 指定用户组
       - -G 指定用户附属组列表，可以指定多项，eg. -G root, adm
       - -a 增加用户的附属组到附属组列表中，必须与-G一起出现，-aG
       - -s 指定用户终端
       - -u 指定用户id，如果不给出，默认是从上一个用户id递增

  2. usermod options username(root)

     - 常用选项与 useradd一致，可以为用户指定新的资源值

  3. userdel options username(root)

     - options：
       - -r 连同用户的根目录一起删除

  4. 用户密码管理: passwd \[optinons] username

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

- **用户组方面**

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

- 新建虚拟终端

  - screen [-S -R name]
  - 不指定终端名，系统会使用linux默认的命名方法，会很麻烦。

  - -R 选项，如果name终端已经存在，则直接连接，如果是-S的话，则会创建一个同名的新终端

- 挂起虚拟终端

  - Ctrl+a d
  - Ctrl+a进入特殊命令模式，在按d键登出

- 连接虚拟终端

  - screen -r -R pid/name
  - -R 选项， 如果终端不存在，则会创建新终端

- 清除虚拟终端

  - 在虚拟终端中Ctrl+d登出，或者输入exit
  
-  在主终端中输入：screen -R pid/name -X quit

- screen -ls 列出所有的虚拟终端
- screen高阶命令：

  - 进入特殊命令模式后：
  - 关闭虚拟终端，相当于exit
  - ？显示所有的命令

### 链接文件
linux中链接文件分为软链接（符号链接）和硬链接。
##### 软链接
`ln -s <源文件> <链接文件>`
软链接相当于指针，会有独一的inode号，有储存空间，其中储存的是源文件的相关信息
##### 硬链接
`ln <源文件> <链接文件>`
硬链接相当于引用（别名），与源文件共享同一inode，只有当所有的硬链接和源文件都被删除时，文件才会被真正删除