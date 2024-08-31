# 注释
- 单行注释
```XML
<!-- commets -->
```
- 多行注释
```XML
<!--
	This 
	is 
	a
	commet
-->
```
# 语法注意点
## 空格
>[!note]
>在XML中，元素内容的前导空格（以及尾随空格）会被视为数据的一部分。XML解析器会保留这些空格，因为它们被认为是元素内容的有效部分。

例如，有以下XML元素：

```xml
<element>    This is some text.</element>
```

元素`<element>`的内容将包括前面的四个空格字符，以及后面的文本“This is some text.”。

如果在处理XML数据时希望忽略这些空格，需要在解析XML之后，使用编程语言提供的字符串处理功能来去除前导和尾随空格。例如，在PowerShell中，可以使用`.Trim()`方法来去除字符串的前导和尾随空格：

```powershell
[xml]$configFile = Get-Content -Path "C:/your/path/config.xml"
$content = $configFile.element.Trim()
```

这将去除`InnerText`属性中字符串的前导和尾随空格。注意，`InnerText`属性获取的是元素及其所有子元素的文本内容，而忽略任何标记。如果你只想获取特定元素的文本内容，并且该元素不包含任何子元素，那么使用`.Trim()`方法是合适的。

## 属性
当一个元素有**属性节点**时，其才具有**文本节点(InnerText)**
```XML
<name>Fenlyin</name>
<!--
访问该元素节点：
Fenlyin
-->

<name id="123">Fenlyin</name>
<!--
访问该元素节点：
id   |#text
-------------
123  |Fenlyin
-->
```