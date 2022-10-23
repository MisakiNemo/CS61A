





**当当前语句中有需要计算的值时，如果该值未被计算或者返回，那么函数在数值返回前不会进行任何其他的操作。这是递归能够存在的本质条件。**

# **Order** **of** **recursive** **function**

**递归函数的一些建议**

![image-20221006213457958](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006213457958.png)

# inverse cascade



# Tree Recursion

![image-20221006214222832](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006214222832.png)

![image-20221006214704318](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006214704318.png)





# Hanoi Question

![image-20221006221511196](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006221511196.png)

**将难的大问题分解成一个简单的问题，这就是递归的魅力**





# counting partitions(这个是重难点)

## question

![问题描述](https://img-blog.csdnimg.cn/0132d77a495743e99042efce7aedc98a.png#pic_center)

## analize

![image-20221007143103024](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007143103024.png)

![image-20221007144753599](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007144753599.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/5735892929474c0c8462e6051af3b4f0.png#pic_center)





## code

![image-20221007143003847](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007143003847.png)







# hw02

## Q1：num eights

Write a recursive function `num_eights` that takes a positive integer `x` and returns the number of times the digit 8 appears in `x`. *Use recursion - the tests will fail if you use any assignment statements.*

### code

```
 if x<10:
        return 1 if x==8 else 0
    else:
        return num_eights(x//10)+num_eights(x%10)
```



## Q2:  pingpong

The ping-pong sequence counts up starting from 1 and is always either counting up or counting down. At element `k`, the direction switches if `k` is a multiple of 8 or contains the digit 8. The first 30 elements of the ping-pong sequence are listed below, with direction swaps marked using brackets at the 8th, 16th, 18th, 24th, and 28th elements:

![image-20221007105455631](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007105455631.png)

### example

```
def pingpong(n):
    """Return the nth element of the ping-pong sequence.

    >>> pingpong(8)
    8
    >>> pingpong(10)
    6
    >>> pingpong(15)
    1
    >>> pingpong(21)
    -1
    >>> pingpong(22)
    -2
    >>> pingpong(30)
    -2
    >>> pingpong(68)
    0
    >>> pingpong(69)
    -1
    >>> pingpong(80)
    0
    >>> pingpong(81)
    1
    >>> pingpong(82)
    0
    >>> pingpong(100)
    -6
    >>> from construct_check import check
    >>> # ban assignment statements
    >>> check(HW_SOURCE_FILE, 'pingpong', ['Assign', 'AugAssign'])
    True
    """
    "*** YOUR CODE HERE ***"
```

### code

#### mine,but timeout

![image-20221007084115934](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007084115934.png)

睡觉睡不着想到的，从这个方法大概知道了**递归是依靠以前的得到的结果来求出结果的一种算法，大致思路就是用前面的值来表示当前值，设立一个条件到达终止值时返回对应的**

#### other

```
    def helper(index):
        if index==1:
            return 1
        elif index%8==0 or num_eights(index)!=0:
            return -helper(index-1)
        return helper(index-1)
    if n==1:
        return 1
    return pingpong(n-1)+helper(n-1)
```

将问题分割成两部分：一部分定义一个辅助递归函数求当前的dir值，一部分利用辅助函数，求当前的pingpong值

**这个问题本质上是，是求三个值间的关系：第一个值（index）规律容易表示，第二个值（dir）随着第一个值的一些特点变化，而需要求的值则随着第二个值变化。**

**因此，这个问题可以分成两部分：一部分是求dir的值，另一部分利用求出来的dir的值求最终值**

**做题目时要清楚变量之间的关系**





## Q3：Missing nums

Write the recursive function `missing_digits` that takes a number `n` that is sorted in increasing order (for example, `12289` is valid but `15362` and `98764` are not). It returns the number of missing digits in `n`. A missing digit is a number between the first and last digit of `n` of a that is not in `n`. *Use recursion - the tests will fail if you use while or for loops.*

#### example

```
def missing_digits(n):
    """Given a number a that is in sorted, increasing order,
    return the number of missing digits in n. A missing digit is
    a number between the first and last digit of a that is not in n.
    >>> missing_digits(1248) # 3, 5, 6, 7
    4
    >>> missing_digits(1122) # No missing numbers
    0
    >>> missing_digits(123456) # No missing numbers
    0
    >>> missing_digits(3558) # 4, 6, 7
    3
    >>> missing_digits(35578) # 4, 6
    2
    >>> missing_digits(12456) # 3
    1
    >>> missing_digits(16789) # 2, 3, 4, 5
    4
    >>> missing_digits(19) # 2, 3, 4, 5, 6, 7, 8
    7
    >>> missing_digits(4) # No missing numbers between 4 and 4
    0
    >>> from construct_check import check
    >>> # ban while or for loops
    >>> check(HW_SOURCE_FILE, 'missing_digits', ['While', 'For'])
    True
    """
```

### code

#### mine

```
代码：自己写的，但是感觉逻辑有点乱，因为这个是凑出来的。原本写的是一个有些许例子通不过的，然后修改通过例子的特殊情况。
de fuc(num,pre_last,count):
        if num<10 and pre_last!=num:
            return count+pre_last-num-1
        else:
            if pre_last!=num%10:
                return fuc(num//10,num%10,count+pre_last-num%10-1)
            else:
                return fuc(num//10,num%10,count)
    if n<10:
           return 0
    return fuc(n,n%10,0)
```

#### other

```
if n < 10:
        return 0
    if n < 100:
        return n % 10 - n // 10 - 1 if n % 10 != n // 10 else n % 10 - n // 10
    return missing_digits(n // 10) + missing_digits(n % 100)
```



## Q4:count coins

Given a positive integer `total`, a set of coins makes change for `total` if the sum of the values of the coins is `total`. Here we will use standard US Coin values: 1, 5, 10, 25 For example, the following sets make change for `15`:

- 15 1-cent coins
- 10 1-cent, 1 5-cent coins
- 5 1-cent, 2 5-cent coins
- 5 1-cent, 1 10-cent coins
- 3 5-cent coins
- 1 5-cent, 1 10-cent coin

Thus, there are 6 ways to make change for `15`. Write a recursive function `count_coins` that takes a positive integer `total` and returns the number of ways to make change for `total` using coins. Use the `next_largest_coin` function given to you to calculate the next largest coin denomination given your current coin. I.e. `next_largest_coin(5)` = `10`.

#### example

```
def next_largest_coin(coin):
    """Return the next coin. 
    >>> next_largest_coin(1)
    5
    >>> next_largest_coin(5)
    10
    >>> next_largest_coin(10)
    25
    >>> next_largest_coin(2) # Other values return None
    """
    if coin == 1:
        return 5
    elif coin == 5:
        return 10
    elif coin == 10:
        return 25

def count_coins(total):
    """Return the number of ways to make change for total using coins of value of 1, 5, 10, 25.
    >>> count_coins(15)
    6
    >>> count_coins(10)
    4
    >>> count_coins(20)
    9
    >>> count_coins(100) # How many ways to make change for a dollar?
    242
    >>> from construct_check import check
    >>> # ban iteration
    >>> check(HW_SOURCE_FILE, 'count_coins', ['While', 'For'])                                          
    True
    """
    "*** YOUR CODE HERE ***"
```

#### code

**视频的话，除了Q&A外，每一部分都要看！**

```
 def count(n,coin):
        if n==0:
           return 1
        elif n<0:
            return 0
        elif coin==None:
            return 0
        return count(n-coin,coin)+count(n,next_largest_coin(coin))
    return count(total,1)
```

##### other

基本思路就是切分成两种，一种是可以使用start_coin，一种是不可以。比如15，可以切分成是否可以使用10这个硬币，第一种可以使用10的话，那就考虑在最大可使用硬币是10的情况下去加成5（15-10）；第二种不能使用10的话，就考虑在最大可使用硬币是5的情况下去加成15

<img src="C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007152119232.png" alt="image-20221007152119232" style="zoom:50%;" />

<img src="C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007152153643.png" alt="image-20221007152153643" style="zoom:50%;" />

![image-20221007152829966](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221007152829966.png)







# 总结

存在问题：

c_p算法仍然不太明白，查了一下大概是离散数学方面的知识

先放着吧