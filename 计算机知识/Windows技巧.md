# winget
## 换源
- `winget source remove <name>` 移除某个名为 `<name>` 的源
- `winget source add <name> <url>` 添加 `<url>` 源，命名为 `<name>`
- `winget source list` 查看源列表
**注：** 源列表中不允许有同名的源

## 指定安装路径
``` powershell
winget install <package.name> -l[--location] D:\app\target.folder
```
需要手动创建软件包根目录

# Excel 乱码问题
> csv 文件 utf-8 编码，使用 Excel打开，汉字全部为方框乱码

**原因：** Excel 默认使用 `UTF-8 BOM` 解析文件。 `UTF-8 BOM` 只是在 `UTF-8` 的基础上在文件头多了  `EF BB BF` 这三个字节。解码错位导致出现了乱码。

# Windows Schedule Tasks
* `/sc`: 指定计划类型。可以是 MINUTE、HOURLY、DAILY、WEEKLY、MONTHLY、ONCE、ONSTART、ONLOGON、ONIDLE 或 ONEVENT。 
* `/tn`: 指定任务的名称。 
* `/tr`: 指定要运行的命令或脚本。 
* `/st`: 指定开始时间。对于 ONCE 计划，这是必需的。 
* `/ed`: 指定任务的结束日期（可选）。

当然，以下是 `schtasks /create` 命令的Markdown格式总结：

## SCHTASKS /Create 命令概述

`SCHTASKS /Create` 命令允许管理员在本地或远程系统上创建计划任务。

## 参数列表

- `/S system`: 指定要连接的远程系统。如果省略，默认为本地系统。
- `/U username`: 指定 SchTasks.exe 应执行的用户上下文。
- `/P [password]`: 指定给定用户上下文的密码。如果省略，将提示输入。
- `/RU username`: 指定任务运行的"作为"用户账户（用户上下文）。对于系统账户，有效值为 `""`, `"NT AUTHORITY\SYSTEM"` 或 `"SYSTEM"`。
- `/RP [password]`: 指定"作为"用户的密码。如果值为 `"*"` 或无，将提示输入密码。对于系统账户，此密码将被忽略。
- `/SC schedule`: 指定计划频率。有效计划类型：`MINUTE`, `HOURLY`, `DAILY`, `WEEKLY`, `MONTHLY`, `ONCE`, `ONSTART`, `ONLOGON`, `ONIDLE`, `ONEVENT`。
- `/MO modifier`: 对计划类型进行细化，以便对计划的重复性进行更精细的控制。
- `/D day`: 指定任务运行的星期几或月份中的哪一天。
- `/M months`: 指定一年中的月份。
- `/I idletime`: 指定在运行计划的 `ONIDLE` 任务之前等待的空闲时间。
- `/TN taskname`: 指定以路径\名称形式的唯一标识符。
- `/TR taskrun`: 指定在预定时间运行的程序的路径和文件名。
- `/ST starttime`: 指定任务开始运行的时间。
- `/RI interval`: 指定重复间隔（分钟）。
- `/ET endtime`: 指定任务运行的结束时间。
- `/DU duration`: 指定任务运行的持续时间。
- `/K`: 在结束时间或持续时间到达时终止任务。
- `/SD startdate`: 指定任务首次运行的日期。
- `/ED enddate`: 指定任务运行的最后日期。
- `/EC ChannelName`: 指定 `OnEvent` 触发器的事件通道。
- `/IT`: 仅当作业运行时 `/RU` 用户已登录，才允许任务交互式运行。
- `/NP`: 不存储密码。作为给定用户非交互式运行任务。
- `/Z`: 在任务最后一次运行后将其标记为删除。
- `/XML xmlfile`: 从指定的 XML 文件创建任务。
- `/V1`: 创建对预 Vista 平台可见的任务。
- `/F`: 强制创建任务并抑制警告。
- `/RL level`: 设置作业的运行级别。
- `/DELAY delaytime`: 指定触发器触发后延迟运行任务的时间。
- `/HRESULT`: 进程退出代码将以 HRESULT 格式显示。
- `/?`: 显示帮助信息。

## 修饰符

- `/MO` 开关的有效值根据计划类型而异。

## 示例
```
schtasks /create /sc DAILY /tn "My Task" /tr "C:\path\to\your\script.bat" /st 08:00 /ed 12/31/2023
```

1. 创建每小时在远程机器 "ABC" 上运行 `notepad.exe` 的任务 "doc"。
   ```
   SCHTASKS /Create /S ABC /U user /P password /RU runasuser /RP runaspassword /SC HOURLY /TN doc /TR notepad
   ```

2. 创建在远程机器 "ABC" 上运行 `calc.exe` 的任务 "accountant"，每五分钟运行一次。
   ```
   SCHTASKS /Create /S ABC /U domain\user /P password /SC MINUTE /MO 5 /TN accountant /TR calc.exe /ST 12:00 /ET 14:00 /SD 06/06/2006 /ED 06/06/2006 /RU runasuser /RP userpassword
   ```

3. 创建每月第一个星期日运行 `freecell` 的任务 "gametime"。
   ```
   SCHTASKS /Create /SC MONTHLY /MO first /D SUN /TN gametime /TR c:\windows\system32\freecell
   ```

4. 创建每周在远程机器 "ABC" 上运行 `notepad.exe` 的任务 "report"。
   ```
   SCHTASKS /Create /S ABC /U user /P password /RU runasuser /RP runaspassword /SC WEEKLY /TN report /TR notepad.exe
   ```

5. 创建每天从指定开始时间运行 `notepad.exe` 且没有结束时间的任务 "logtracker"。
   ```
   SCHTASKS /Create /S ABC /U domain\user /P password /SC MINUTE /MO 5 /TN logtracker /TR c:\windows\system32\notepad.exe /ST 18:30 /RU runasuser /RP
   ```

6. 创建每天从 12:00 开始运行 `freecell.exe` 并在 14:00 自动终止的任务 "gaming"。
   ```
   SCHTASKS /Create /SC DAILY /TN gaming /TR c:\freecell /ST 12:00 /ET 14:00 /K
   ```

7. 创建当系统事件通道发布事件 101 时运行 `wevtvwr.msc` 的任务 "EventLog"。
   ```
   SCHTASKS /Create /TN EventLog /TR wevtvwr.msc /SC ONEVENT /EC System /MO *[System/EventID=101]
   ```

8. 处理文件路径中空格的示例。
   ```
   SCHTASKS /Create /tr "'c:\program files\internet explorer\iexplorer.exe' 'c:\log data\today.xml'" ...
   ```
