
# DOS访问环境变量
## 修改
使用 `setx` 命令
``` batch
:: set
setx test "hello"
:: add
setx test "%test%;world"
```
- dos使用setx第一次访问环境变量，都会同时创建与环境变量同名的局部变量，这也是改变环境变量需要重启才能输出修改之后值的原因（旧的局部变量优先级大于环境变量\[就近原则])。
- powershell则完全不会创建局部变量。

## 访问
```batch
:: 列出所有的环境变量和值
set

:: 访问指定变量
echo %paht%  :: 访问 paht 变量
```


# powershell访问环境变量。
``` powershell
# 访问
$var=[Environment]::getEnvironmentVariable(name:str, host:Union("User"|"Machine"))
# 设置
[Environment]::setEnvironmentVariable(name, value:str, host)
```
两者都需要通过特殊方式访问环境变量，然后再局部创建和环境变量同名的局部变量。


# Cmd 设置代理服务器
一帮情况下，cmd 不会走系统代理，即使你开启了系统代理。可以设置环境变量来实现系统代理：
- `http_proxy=http://127.0.0.1:7897`
- `https_proxy=http://127.0.0.1:7897`

