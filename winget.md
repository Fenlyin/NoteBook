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