### 创建线程
``` python
t1 = Thread(target=func()) # 创建线程
```

### 开始线程
``` python
t1.start()
```

### 等待线程结束
``` python
t1.join()
```

在多线程中，有时线程之间需要有一定的执行顺序，或者为了解决资源竞争，必须使某个线程结束后才能开始执行另一个线程，这时就需要使用 `join()` 函数了
