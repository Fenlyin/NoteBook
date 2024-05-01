# 查看当前用户：
<center> 
SELECT CURRENT_USER();
</center>

# 创建用户（当拥有创建权限时）:
<center>
CREATE 'username '@'hostname' IDENTIFIED BY 'password';	
</center>

# mysql 表结构
`DESC <TABLE_NAME>`
- `Field` 表中的字段，相当于一个对象有哪些属性
- `Type` 对应属性值的类型
- `Key` 对应字段是什么键（主键/外键等）
- `Default` 对应字段的默认值
- `Extra` 对应字段的额外描述信息
- `Null` 对应字段值是否可以为 `null`， `YES` 表明允许
![](table_structure.png)
`Country`表有15个字段。

mysql中的基本单元是表，多张表组成数据库。