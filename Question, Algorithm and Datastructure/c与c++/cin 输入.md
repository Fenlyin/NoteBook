### cin >> value;

cin对象的bool值可行的原因是基类basic_ios对operator bool（）有重载；

当其缓冲区遇到的值类型与value的值类型不一致时，cin对象的bool值为false，这可以作为循环或条件语句的条件。

eg.

&nbsp; while(cin >> arr\[i++\]);