# 箭头函数 =>
`func = para => para * para`等价于 :
``` js
function func(para){
	return para * para
}

func = (a, b) => { 
let i = 1; ({"name": a, "age": b}) 
}
// 1. 当有多个参数时，使用圆括号
// 2. 当有多条语句时，使用花括号
// 3. 当需要返回对象时，为了和语句块区分，需要将对象用圆括号包裹
```
箭头函数中的this对象是定义函数时的对象，而不是调用函数时的对象
# ... 运算符
相当于python中的解包
- `...iterable` 把iterable解包为以逗号分隔的seqence
- `...seqence` 把seqence 合并为一个iterable，常用于函数的不定长参数

# 数据类型
## 基本数据类型
1. `Boolean`
2. `Number`
3. `String`
4. `Undefined`
5. `Symbol`
6. `Bignum`

## 复合数据类型
1. `Function`
2. `Object`
	- `Array`
	- `Date`
	- `RegExp`

注：`null` 是 `object` 类型对一个**常量**。
# DOM接口
DOM 模型将HTML文件描述为树结构，树的节点分为三种类型： 元素节点、文本节点、属性节点。
- `ele.childNodes` 返回元素的所有子元素节点、文本节点
- `ele.children` 返回元素的所有子元素节点
- `ele.attributes` 返回元素的所有属性节点

# 对象Object 属性名
`Object` 的属性名只有`String`和`Symbol`两种类型，`Symbol`保证该属性是唯一的。

当在定义对象时如果给的属性名为其他非字符串类型（如数值型），则会**隐式转换**为字符串类型。
# 数组是特殊的对象
```Javascript
arr = new Array(1, 2, 3);
for (i in arr){
	console.log(typeof(i));
}
// output:
// string
// string
// string
```
即数组是以自身索引为属性名的对象。