# SpringBoot 项目创建
## 利用 Idea 插件快速创建
![](Pasted%20image%2020240909185357.png)


# SpringBoot 配置文件
有两种类型的配置文件`application.properties`和`application.yml`. 一般常用`yaml`文件作为配置文件 , 因为结构清晰。

## 获取配置文件中的数据
1. `@Value`
```Java
@Value("server.port")
public string var;

// 将配置文件中的 server.port 值赋值给变量 var
```

2. `@configurationProperties`
```Java
@configurationProperties(prefix = "server")
public class Test(){
	// 变量 port 的值就是 serever.port 的值
	// 变量名必须和配置文件中的键一致
	// 变量必须要有 setter() 函数
	public string port;	

	public void main(){
		...;
	}
}
```

使用 `@configurationProperties` 注解更加简便.
