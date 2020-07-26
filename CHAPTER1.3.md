数据结构时间、空间复杂度

时间复杂度：**表达算法执行效率与数据规模增长的趋势**

假设：每条语句运行时间为 unit_time ，运行语句的条数为 n ，那么总时间就为：n * unit_time

例子如下：


```
var add = function(n) {
    let b = 1;
    for (let i=0; i<n: i++) {
        b++;
    }
    return b;
}
```

注：这是由 javascript 书写的代码，当然，这段代码是用来辅助说明时间复杂度表示的本质：**表达算法执行效率与数据规模增长的趋势**。

如上程序， O(f(n))=O(1+n) , 而 f(n) 中的低阶、常量、系数是不左右趋势的。所以，O(1+n)=O(n)。

那，有多少种不同的趋势呢？
六种：

> * 常数：O(1)
> * 对数：O(logn)
> * 线性：O(n)
> * 线性对数：O(nlogn)
> * 指数：O(2^n)
> * 阶乘阶：O(n!)

![时间随数据规模增长的趋势图](https://static001.geekbang.org/resource/image/49/04/497a3f120b7debee07dc0d03984faf04.jpg)

下面，介绍一下两种较难理解的增长趋势：O(logn)、O(nlogn)

时间复杂度为 O(logn)，对应代码如下：

```
var add = function(n) {
    int b = 1;
    while (b < n) {
        b *= 2;
    }
    return b;
}
````

而时间复杂度 O(nlogn)，显然就是 O(n) O(logn) 的嵌套

```
var add = function(n) {
    int b = 1;
    for (lei i=0; i<n; i++) {
        while (b < n) {
            b *=2;
        }
    }
    return b;
}
```