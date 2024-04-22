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