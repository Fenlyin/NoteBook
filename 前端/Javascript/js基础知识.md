### 箭头函数 =>
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
- 箭头函数中的this对象是定义函数时的对象，而不是调用函数时的对象
### ... 运算符
相当于python中的解包
- `...iterable` 把iterable解包为以逗号分隔的seqence
- `...seqence` 把seqence 合并为一个iterable，常用于函数的不定长参数