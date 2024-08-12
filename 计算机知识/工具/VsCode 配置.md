-  一键编译并运行(debug mode)： `F5`
-  一键编译并运行(not debug mode)： `Ctrl + F5`

# settings.json file
- `~\AppData\Roaming\Code\User\settings.json` 全局配置文件，包含各种插件配置（仅包含开启同步功能的属性）、vscode本身的配置（如字体、字号等）。
- `${workspace}\.vscode\settings.json` 工作区局部配置文件，只影响当前工作区，优先级大于全局配置。
- settings其实相当于一个**云端备份文件**，主要备份一些插件设置；**自动提示功能由插件settings中的description给出**；文件内容的上下顺序跟插件某属性**开启备份功能的先后有关**。
- vscode会在启动时以及启动后定期“执行”（触发事件应该还有很多）settings.json 和 工作区的settings.json，目的是实时更新设置。


## snippets 详解
### snippet defination
```json
"name":{
	"prefix":"your prefix",
	"body":["your snippet body"], // 列表中一个元素占一行 
	"isFileTemplate": true | false // 是否作为文件模板，如果是文件模板，那么该snippet将生成一个特定的初始文件
}
```

![](snippets.png)
- `debug1` 是匹配前缀
- `debug123` 是该Snippet的标题
- 详情页第一行是decription，后面的括号表明这是一个用户自定义的Snippet；第二行是该Snippet的具体内容（body）


## variables
With `$name` or `${name:default}`, you can insert the value of a variable. With `${name|var1, var2, var3|}`, you can select the value of a variable when you insert it, or assign a new value.

- `${1:var}` 数字`1...9` 表示光标所在placeholder的次序，冒号后面的是默认值
- `${0:var}` 数字`0`标识最后一个placeholder
- `${1|var1, var2, var3|}` you can select from the list, or assign a new value