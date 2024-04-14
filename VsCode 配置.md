-  一键编译并运行(debug mode)： `F5`
-  一键编译并运行(not debug mode)： `Ctrl + F5`

### settings.json file
- `~\AppData\Roaming\Code\User\settings.json` 全局配置文件，包含各种插件配置（仅包含开启同步功能的属性）、vscode本身的配置（如字体、字号等）。
- `${workspace}\.vscode\settings.json` 工作区局部配置文件，只影响当前工作区，优先级大于全局配置。
- settings其实相当于一个**云端备份文件**，主要备份一些插件设置；**自动提示功能由插件settings中的description给出**；文件内容的上下顺序跟插件某属性**开启备份功能的先后有关**。
- vscode会在启动时以及启动后定期“执行”（触发事件应该还有很多）settings.json 和 工作区的settings.json，目的是实时更新设置。