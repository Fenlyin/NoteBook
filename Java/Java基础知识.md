## Java包装类
**主要目的：**使基本数据类型能够像对象一样，调用属性和方法，并通过调用自身方法实现类型转换（包括与字符串之间的相互转换）。

### 装箱与拆箱
将基本数据类型包装为类的过程称为装箱，装箱分为手动装箱和自动给装箱。
```Java
int x = 1;
Integer x1 = new Integer(x); // 手动装箱
Integer x2 = x; // 自动装箱
```

从已包装的类得到基本数据类型的过程称为拆箱，同样，拆箱分为手动拆箱和自动拆箱。
```Java
int y1 = x1.intValue(); // 手动拆箱
int y2 = x1; // 自动拆箱
```
每个基本数据类型的包装类都有一个形如`xxxValue()`的方法，用于手动拆箱操作。

### 通过包装类实现类型转换
#### valueOf() 
想要转换为何种类型，就调用该类型的类方法`valueOf()`。e.g.
```Java
int a = 10;
double b = Double.valueOf(a); // 将int型 a 转为double型 b
```
_**notice**_: 
1. 通过`valueOf()`进行基本数据类型之间的相互转换时，只能从高精度往低精度转。
2. 

#### 与字符串之间的转换
**数据类型转字符串：**  
String.valueOf(\<var>)

\<type>.to_String(\<var>)

**字符串转为基本数据类型：**
\<type>.parseXXX()


## 连接MySQL数据库
