# css计数器
## counter and counters
- counter(\<name>) 返回指定计数器的值
- counters(\<name>, str) 返回所有名称为 `<name>` 的计数器的值，从最外层开始调用，多个值之间使用 `str` 连接

# 属性选择器
## 存在性选择

```css
tag[attr] {

}
// 选择存在 attr 属性的 tag 元素
```

## 值选择器

```css
 tag[attr=value] {
    
}
// 选择存在 attr 属性且值为 value 的 tag 元素
```

# 表单
## form 元素
- `action` 该属性表示表单最终要提交到何处，由 `submit` 类型的 `input` 元素触发