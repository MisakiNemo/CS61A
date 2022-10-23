# Iterators

![image-20221013090651404](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013090651404.png)

**迭代器，c++中说可以像指针一样理解**

**不理解的点：StopIteration**



# Dictionary Iterators

![image-20221013091349262](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013091349262.png)

![image-20221013091713445](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013091713445.png)

**知识点**

我的理解上：当将一个迭代器当成一个容器（列表、字典）来使用（查看，修改）的时候，那么该迭代器就不能够再当成迭代器使用，只能当成一个容器来使用了

另外里面提到：容器的每个元素的值的更改不会影响迭代器的使用，但是容器的长度（大小）的改变会导致改变之前的所有的迭代器都不能够使用

# For Statement

![image-20221013092300576](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013092300576.png)

一句话就是，使用迭代器for循环遍历，那么迭代器的指向会不断推进，直到末尾而无法继续使用。但是若正常遍历容器而不是使用迭代器，那么可以多次使用

# Built-in Iterator Functions

![image-20221013093357457](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013093357457.png)

## map

<img src="C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013093536601.png" alt="image-20221013093536601" style="zoom:50%;" /><img src="C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013094327765.png" alt="image-20221013094327765" style="zoom: 80%;" />

返回一个迭代器，每次调用这个迭代器，都会对容器中的每个数据调用生成迭代器时传入的函数并返回结果

![image-20221013104022578](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013104022578.png)

# Generators（生成器）

![image-20221013105022056](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013105022056.png)

看起来定义与常规函数无异，唯一的区别在于yield。这种函数返回的是一个迭代器。当第一次调用这个迭代器时，会运行生成器里面的语句。当遇到yield时返回数据，并且保存当前环境。第二次调用时，会接着上一次调用时运行到的地方继续运行，并且在遇到yield返回，如此循环往复。另外当将返回的迭代器传入list中，会返回生成器函数里面所有返回的数值

# Generators&Iterators

生成器经常在运行的时候传入迭代器

#### 递归使用生成器

![image-20221013111547129](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013111547129.png)





![image-20221013111425523](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013111425523.png)

substring有点懵

```
for i in iterator==yield from iterator
```

列表的slicing用法若参数为负数，那么代表的是从列表的最后一个元素开始计算，最后一个元素的下标为-1
