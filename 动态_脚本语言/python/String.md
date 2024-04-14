### encode/decode
```python
s = "hello world"
s_utf = s.encode("utf-8")
s_utf_utf = s_utf.decode("utf-8")
```
### 任意进制转十进制
`int(num:str, base:int)`
- `num:` base进制的数字