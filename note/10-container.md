# List

![image-20221007153440805](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007153440805.png)

```
len:求数组的长度，元素个数
选取下标为n的元素：digits[n] or getitem(digits,n)
列表相乘相加：只会将多个链表中的元素相加成一个链表，相加后的链表中每个元素的值并不会改变
容器可以嵌套使用
```

# Container

![image-20221007154128797](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007154128797.png)

**判断元素x是否在容器digits中： x in digits，返回值为bool**

**但是这个寻找语句只会一个一个元素寻找，不会嵌套寻找（如最后一个例子）**





# For statement

![image-20221007220231655](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007220231655.png)





# Range

**range通常用来表示一串连续的**

![image-20221007222803137](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007222803137.png)



![image-20221007222909910](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007222909910.png)

**若是只是关心循环的次数而不需要使用到变量，那么可以用下划线(_)来代替参数**





# Recursion sums

![image-20221007223631124](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007223631124.png)

L[1:]的意思是从下标1到列表结尾。

**一般使用方法是：list[start::end],但是，并不包括list[end]**





# List comprehensions

![image-20221007224931600](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007224931600.png)

```
对遍历返回的数进行操作： [state for x in list]
对返回的数进行筛选和操作： state for x in list if condition 
```





# String

![image-20221007225507544](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007225507544.png)

```
exec(string):运行一个string语句
```





## String Reverseal

![image-20221007230649665](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007230649665.png)

递归翻转字符串





# lab04

## Q1

```
 lst = [3, 2, 7, [84, 83, 82]]
>>> lst[4]
>>>error
输出为错误，当下标超过list长度时
```







## Q2

![image-20221008084152331](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221008084152331.png)

### code

```
 if n<=0:
        return 0
    else:
        return n+skip_add(n-2)
```





## Q3

![image-20221008084557146](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221008084557146.png)

### code

```
 assert n >= 1
    "*** YOUR CODE HERE ***"
    if n==1:
        return term(1)
    else:
        return term(n)+summation(n-1,term)
```





## Q4：paths

![image-20221008091030978](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221008091030978.png)

### code

```
    if m==1 or n==1:
        return 1
    else:
        return paths(m-1,n)+paths(m,n-1)
```

## Q4

![image-20221008091411336](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221008091411336.png)

```
def max_subseq(n, t):
    """
    Return the maximum subsequence of length at most t that can be found in the given number n.
    For example, for n = 20125 and t = 3, we have that the subsequences are
        2
        0
        1
        2
        5
        20
        21
        22
        25
        01
        02
        05
        12
        15
        25
        201
        202
        205
        212
        215
        225
        012
        015
        025
        125
    and of these, the maxumum number is 225, so our answer is 225.

    >>> max_subseq(20125, 3)
    225
    >>> max_subseq(20125, 5)
    20125
    >>> max_subseq(20125, 6) # note that 20125 == 020125
    20125
    >>> max_subseq(12345, 3)
    345
    >>> max_subseq(12345, 0) # 0 is of length 0
    0
    >>> max_subseq(12345, 1)
    5
    """
    "*** YOUR CODE HERE ***"
```

![image-20221008091444809](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221008091444809.png)

### code