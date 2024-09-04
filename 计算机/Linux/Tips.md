### 在shell中给出python代码，并执行
##### shell
``` shell
# 通过 HereDoc 给出多行字符串作为源代码
python <<EOF
>x = 1
>print(x)
>EOF


```

``` shell
# 如代码只有一行：
python -c "print('Hello World')"
```
##### powershell
``` powershell
# Here-String
python -c @"
>x = 1
>print(x)
>"@
```

