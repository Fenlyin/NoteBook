###  查找与替换
1. **查找**：`/{pattern}`模式输入完毕后按`Enter`或`Esc`退出查找输入模式，接下来按`n` 查找符合模式的下一个字符串，按`N`查找符合模式的上一个字符串，除非重新输入模式串，否则已经输入的模式会保存，一直生效。
2. **替换：** `:[range]s/pattern/string/[g]` 
	- `[range]` 以行为单位，一个区间，例如：`2,5`表示\[2, 5]行
	- `pattern`为正则表达式
	- `string`为普通字符串
	- `[g]` 全区修饰符，生效后对一行内**所有**匹配到的字符串进行替换。
	- 严格意义上来说应该为 **批量替换**，即以每一行为一个字符串，而不是将整个文件内容作为一个字符串

### nvim 进入 diff 模式
``` shell
nvim -d file1.txt file2.txt
```

## 快速在行间跳转
- `:line_number` 按绝对行号跳转
- `:+ | - line_number` 按相对行号跳转
- `:percentage` 按百分比跳转
- `:m<tag>  :'<tag>` 按标记跳转。使用`m`做标记，使用`'`跳到指定标记所在的行

## 高亮指定单词
### match
```vimrc
match ErrorMsg /ERROR/
```
这样，`ERROR`将使用`ErrorMsg`高亮组的规则高亮，为红色背景。
match 只能生效一个，若有多个高亮模式，则应使用matchadd
### matchadd 
```vimrc
call matchadd('search', 'TODO')
call matchadd('ErrorMsg', 'error')
" 具体语法
" call matchadd(hlGroup, Pattern)
```

### 搜索高亮
此种方法不太完善
```vimrc
set hlsearch
```
首先要开启搜索高亮，之后搜到单词就高亮，但一旦改变`/`寄存器的内容，高亮单词也随之改变，所以不完善

### syntax
。。。使用自定义高亮组和syntax命令，但还不太清除，待补充


## 分屏
### 在缓冲区分屏
- 垂直分屏：`:vsplit [file]` or `:vsp [file]` or `<C-w> v`
- 水平分屏：`:split [file]` or `:sp [file]` or `<C-w> s`

### 启动时分屏
- 垂直分屏：`vim -On file1 file2 ...` 
- 水平分屏：`vim -on file1 file2 ...` 
其中，`n`是分屏个数，如果不指定，有多少个文件就分几个屏，如果指定，多出来的会打开新文件(unamed)。

### 屏幕相关的操作
1. 移动光标
`<C-w> k | j | h | l`
2. 移动屏幕
`<C-w> K | J | H | L`
3. 改变屏幕大小
	- `<C-w> +` 增加屏幕高度
	- `<C-w> -` 减小屏幕高度
	- `<C-w> >` 增加屏幕宽度
	- `<C-w> <`  减小屏幕宽度
	- `<C-w> =` 初始化所有屏幕的尺寸
4.  关闭屏幕
	- `<C-w> c` 关闭屏幕，最后一个除外
	- `<C-w> q` 关闭屏幕，最后一个也可以关闭


## 寄存器
### 寄存器类型
1. 匿名寄存器（`""`）
2. 编号寄存器(`"0-9`)
3. 小删除寄存器 (`"-`)
4. 命名寄存器 (`"a-z`)
5. 只读寄存器 (`":`, `".`,and `"%`)
6. Buffer交替文件寄存器 (`"#`)
7. 表达式寄存器 (`"=`)
8. 选取和拖放寄存器(`"*` and `"+`)
9. 黑洞寄存器 (`"_`)
10. 搜索模式寄存器 (`"/`)
查看所有存在值的寄存器：`:register`

### 寄存器输出
1. Normal mode: `<C-r> <reg>`
2. Insert mode: `"<reg><p>`
3. Normal mode: `:put <reg>`

### 寄存器输入
1. Normal mode or Visual mode: `"<reg><y>`

