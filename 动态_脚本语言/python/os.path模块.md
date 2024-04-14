- `join(str:arg* para) -> str` 将参数按从左到右的的顺序组合成有效的文件路径
``` python
>>>os.path.join('var', 'log', 'cron.log')
'var/log/cron.log'
>>>os.path.join('/', 'var', 'log', 'cron.log')
'/var/log/cron.log' # '/'作为根目录
>>>os.path.join('sys', '/', 'var', 'log', 'cron.log')
'/var/log/cron.log' # '/'之前的参数会无效
### 在windows环境下，'/' 会变为'\\'
>>>os.path.join('sys', '/', 'var', 'log', 'cron.log')
'/var\\log\\cron.log'
```
- `dirname(str:path) -> str` 传入一个文件路径，返回去掉叶子节点后的路径
``` python
>>>os.path.dirname('/var/log/cron.log')
'/var/log'
```
- `basename(str:path) -> str` 传入一个文件路径，返回叶子节点
``` python
>>>os.path.basename('/var/log/cron.log')
'cron.log'
```