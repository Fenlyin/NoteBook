## assert statement
``` python
x = 'hello'
assert x == 'world'[,'x is not world']
```
The `assert` statement is used to debug whether a specified expression is `True` or `False`. If the expression evaluates to `True`, nothing will happen. Otherwise, an `AssertionError` will be raised. Additionally, you can customize the exception information by adding `, 'your custom error info'` at the end of the `assert` statement.

## encode/decode
```python
s = "hello world"
s_utf = s.encode("utf-8")
s_utf_utf = s_utf.decode("utf-8")
```
## 任意进制转十进制
`int(num:str, base:int)`
- `num:` base进制的数字

## for 循环底层原理
- 可迭代对象：实现了`__iter__()`方法的对象
- 迭代器：实现了`__next__()`方法的对象

一般情况下，可迭代对象会使用`__iter__()`方法返回一个迭代器对象（即实现了`__next__()`方法，之后由该迭代器来迭代自己。

## 装饰器、迭代器与生成器
### 装饰器
- 装饰器本质是一个函数。装饰器（函数）接受一个函数参数，对这个函数的功能进行**扩展**，之后返回一个扩展功能后的新的函数。
- 使用装饰器的好处是：先定义实现基本功能（需要已确定）的函数，在通过装饰器对基本函数进行装饰，实现各种高级功能， **应对未知需求**。
``` python
def calculate_time(func): # 装饰器
    def wrapper(num:int): # 这将是装饰后的函数
        start = time.time()
        time.sleep(1)
        res = func(num)
        end = time.time()
        return res, end - start # 扩展了被装饰函数的功能
    return wrapper # 返回装饰后的函数


@calculate_time
def factorial1(num:int): # 递归函数不推荐装饰
    if num == 0:
        return 1
    else:
        return num * factorial1(num-1)

        
@calculate_time # 被装饰后其功能得到扩展
def factorial(num:int): # 只实现了基本功能的函数
    if num == 0:
        return 1
    else:
        res = 1
        for i in range(1, num + 1):
            res *= i
    return res
```
- 递归实现的函数一般不容易被装饰。

## 多线程与线程安全
当某个操作为原子(`atomic`)时，这个操作是线程安全的。操作线程安全是说：在执行这个操作中途不会调度到另一个线程，避免了共享数据的混乱。

对于非线程安全型操作，可以手动加锁，使其线程安全
``` python
from threading import Thread
import threading

num = 0
lock = threading.RLock()

def task1():
    lock.acquire()
    for i in range(1000000):
        global num
        num += 1
    lock.release()
	
def task2():
    lock.acquire()
    for i in range(1000000):
        global num
        num -= 1
    lock.release()

t1 = Thread(target=task1)
t2 = Thread(target=task2)

t1.start()
t2.start()
t1.join()
t2.join()
print(num)
```
考虑一下场景：
- `task1: r <- 0(num)`
- `task2: r <- 0(num)`
- `task2: r--(-1)`
- `task2: num <- r(-1)`
- `task1: r++(1)`
- `task1: num <- r(1)`
最终，`num == 1`， 显然不符合预期，因为 `+=` 和 `-=` 是非线程安全的，所以手动加锁才行。

## 递归锁与死锁
在python中，有两种锁：
1. `threading.RLock()` 递归锁，允许多次获取和释放
2. `threading.Lock()` 普通锁，只允许获取一次
### RLock应用案例
``` python	
lock = treading.RLock()
def my_func():
	lock.acquire()
	pass
	lock.release()

def other_func():
	lock.acquire()
	my_func() # 多次获得锁
	lock.release()
```

### 死锁
定义：永远不能被获取的锁成为死锁