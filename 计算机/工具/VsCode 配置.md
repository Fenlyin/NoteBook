-  一键编译并运行(debug mode)： `F5`
-  一键编译并运行(not debug mode)： `Ctrl + F5`

# settings.json file
- `~\AppData\Roaming\Code\User\settings.json` 用户配置文件，设置中修改过的项目会保存在这个文件中，达到备份作用，没有修改过的项目，则无需保存，因为每个设置都有默认值。
- `${workspace}\.vscode\settings.json` 工作区局部配置文件，只影响当前工作区，优先级大于全局配置。
- vscode会在启动时以及启动后定期“执行”（触发事件应该还有很多）settings.json 和 工作区的settings.json，目的是实时更新设置。


# snippets 详解
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


## .vscode
- `task` 相当于批处理，自动化程序
- `launch` 预定义的一些启动任务


# tasks
```json
{
    "version": "2.0.0",
    "tasks":[
        { // task 1
            "label": "Deploy",
            "type": "shell",
            "command": "_deploy ${workspaceFolder}",
            "detail": "Deploy the web application",
            "presentation": {
                "echo": true,
                "reveal": "never",
                "focus": true,
                "panel": "shared",
                "showReuseMessage": false,
                "clear": false
            }
        },
        { // task 2
            "label": "test",
            "type": "shell",
            "command": "echo ${userHome}",
            "presentation": {
                "echo": true,
                "reveal": "never",
                "focus": true,
                "panel": "shared",
                "showReuseMessage": false,
                "clear": true
            }
        }
    ]
}
```


# launch
```json
{
    "configurations": [
        { // launch 1
            "name": "Launch WebApp",
            "type": "chrome",
            "request": "launch",
            "preLaunchTask": "Deploy",
            // "postDebugTask": "Finished",
            "url": "http://localhost:8080/HELLO/index.html",
        },
        { // launch 2
            "name": "Attach to WebApp",
            "type": "chrome",
            "request": "launch",
            "preLaunchTask": "test"
        }

    ]
}
```

