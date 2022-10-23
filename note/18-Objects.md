## Class and Object

**类**：**A class combines(and abstracts) datas and functions**

**对象**：**An object is an instraction of a class**

![image-20221013122232738](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013122232738.png)

整型是class，有数据和函数（加减乘除）

## Constructor

![image-20221013122750694](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013122750694.png)





# Object-Oriented Programming

![image-20221013141921047](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013141921047.png)

将





# Class Statements

## Object Constructor

![image-20221013143150740](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013143150740.png)

## Object Identity

![image-20221013143433371](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013143433371.png)

self相当于cpp中的this



# Methods

![image-20221013143930804](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013143930804.png)

类中的方法（函数）并没有与类绑定成函数的关系，而是作为一种属性与类绑定，也就是常用的逗号调用的方式



## Invokeing Methods

![image-20221013144347923](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013144347923.png)

调用方法的第一个参数实际上是调用者本身，其次才是其他的参数



## Dot Expressions







# Attributes

## Methods and Functions

![image-20221013145821455](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013145821455.png)

函数+对象=方法





## Looking up Attributes by Name

![image-20221013145942577](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013145942577.png)

首先是判断exp，搜寻exp的地址。然后在该地址上寻找name属性是否存在。如果不存在，那么就会到类（class）中搜寻。若存在参数否则会返回，如果是函数，则会返回这个函数







## Class Attrubutes(类属性/公共属性)

![image-20221013150214084](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013150214084.png)

在类中直接定义的变量是一个公共属性，所有同类型的对象会共享该变量。该变量改变的时候，所有对象中的该变量都会改变







# Homework 4: Nonlocal, Iterators

## Nonlocal

### Q1: Make Bank

Write a new function `make_bank`, which should create a bank account with value `balance` and should also return another function. This new function should be able to withdraw and deposit money. The second function will take in two arguments: `message` and `amount`. When the message passed in is `'deposit'`, the bank will deposit `amount` into the account. When the message passed in is `'withdraw'`, the bank will attempt to withdraw `amount` from the account. If the account does not have enough money for a withdrawal, the string `'Insufficient funds'` will be returned. If the `message` passed in is neither of the two commands, the function should return `'Invalid message'` Examples are shown in the doctests.

#### code

```
def make_bank(balance):
    """Returns a bank function with a starting balance. Supports
    withdrawals and deposits.

    >>> bank = make_bank(100)
    >>> bank('withdraw', 40)    # 100 - 40
    60
    >>> bank('hello', 500)      # Invalid message passed in
    'Invalid message'
    >>> bank('deposit', 20)     # 60 + 20
    80
    >>> bank('withdraw', 90)    # 80 - 90; not enough money
    'Insufficient funds'
    >>> bank('deposit', 100)    # 80 + 100
    180
    >>> bank('goodbye', 0)      # Invalid message passed in
    'Invalid message'
    >>> bank('withdraw', 60)    # 180 - 60
    120
    """
    def bank(message, amount):
        "*** YOUR CODE HERE ***"
        nonlocal balance
        if message=='deposit':
            balance+=amount
            return balance
        elif message=="withdraw":
            if balance>=amount:
                balance-=amount
                return balance
            else:
                return 'Insufficient funds'
        else:
            return 'Invalid message'
    return bank
```





### Q2: Password Protected Account

Write a version of the `make_withdraw` function shown in the previous question that returns password-protected withdraw functions. That is, `make_withdraw` should take a password argument (a string) in addition to an initial balance. The returned function should take two arguments: an amount to withdraw and a password.

A password-protected `withdraw` function should only process withdrawals that include a password that matches the original. Upon receiving an incorrect password, the function should:

1. Store that incorrect password in a list, and
2. Return the string 'Incorrect password'.

If a withdraw function has been called three times with incorrect passwords `<p1>`, `<p2>`, and `<p3>`, then it is frozen. All subsequent calls to the function should return:

#### code

```
    error=[]
    def withdraw(amount,pwd):
        nonlocal password,balance,error
        if len(error)==3:
            return 'Frozen account. Attempts: '+str([s for s in error])
        if pwd==password:
            if balance>=amount:
                balance-=amount
                return balance
            else:
                return 'Insufficient funds'
        else:
            error.append(pwd)
            return 'Incorrect password'
    return withdraw
```

字符串只能与字符串运算相加，可以用str()转换非字符串数据





## Iterators and Generators

### Q3: Repeated

Implement a function (not a generator function) that returns the first value in the iterator `t` that appears `k` times in a row. As described in lecture, iterators can provide values using either the `next(t)` function or with a for-loop. Do not worry about cases where the function reaches the end of the iterator without finding a suitable value, all lists passed in for the tests will have a value that should be returned. If you are receiving an error where the iterator has completed then the program is not identifying the correct value. Iterate through the items such that if the same iterator is passed into `repeated` twice, it continues in the second call at the point it left off in the first. An example of this behavior is shown in the doctests.



#### code

```
def repeated(t, k):
    """Return the first value in iterator T that appears K times in a row. Iterate through the items such that
    if the same iterator is passed into repeated twice, it continues in the second call at the point it left off
    in the first.

    >>> s = iter([10, 9, 10, 9, 9, 10, 8, 8, 8, 7])
    >>> repeated(s, 2)
    9
    >>> s2 = iter([10, 9, 10, 9, 9, 10, 8, 8, 8, 7])
    >>> repeated(s2, 3)
    8
    >>> s = iter([3, 2, 2, 2, 1, 2, 1, 4, 4, 5, 5, 5])
    >>> repeated(s, 3)
    2
    >>> repeated(s, 3)
    5
    >>> s2 = iter([4, 1, 6, 6, 7, 7, 8, 8, 2, 2, 2, 5])
    >>> repeated(s2, 3)
    2
    """
    assert k > 1
    "*** YOUR CODE HERE ***"
    def helper(num,pre=0,count=k-1):
        for i in num:
            if i==pre:
                if count==1:
                  yield i
                else:
                    yield from helper(num,i,count-1)
                yield  from helper(num)
            else:
                yield from helper(num,i)
    re=helper(t)
    return  next(re)
```

##### other

```
    last = next(t)
    occur_times = 1
    for v in t:
        if v == last:
            occur_times += 1
            if occur_times == k:
                return v
        else:
            occur_times = 1
            last = v
```



感觉生成器跟递归差不多





### Q4: Generate Permutations（我不会啊啊啊）（重点）

Given a sequence of unique elements, a *permutation* of the sequence is a list containing the elements of the sequence in some arbitrary order. For example, `[2, 1, 3]`, `[1, 3, 2]`, and `[3, 2, 1]` are some of the permutations of the sequence `[1, 2, 3]`.

Implement `permutations`, a generator function that takes in a sequence `seq` and returns a generator that yields all permutations of `seq`.

Permutations may be yielded in any order. Note that the doctests test whether you are yielding all possible permutations, but not in any particular order. The built-in `sorted` function takes in an iterable object and returns a list containing the elements of the iterable in non-decreasing order.

#### code

```
def permutations(seq):
    """Generates all permutations of the given sequence. Each permutation is a
    list of the elements in SEQ in a different order. The permutations may be
    yielded in any order.

    >>> perms = permutations([100])
    >>> type(perms)
    <class 'generator'>
    >>> next(perms)
    [100]
    >>> try: #this piece of code prints "No more permutations!" if calling next would cause an error
    ...     next(perms)
    ... except StopIteration:
    ...     print('No more permutations!')
    No more permutations!
    >>> sorted(permutations([1, 2, 3])) # Returns a sorted list containing elements of the generator
    [[1, 2, 3], [1, 3, 2], [2, 1, 3], [2, 3, 1], [3, 1, 2], [3, 2, 1]]
    >>> sorted(permutations((10, 20, 30)))
    [[10, 20, 30], [10, 30, 20], [20, 10, 30], [20, 30, 10], [30, 10, 20], [30, 20, 10]]
    >>> sorted(permutations("ab"))
    [['a', 'b'], ['b', 'a']]
    """
    "*** YOUR CODE HERE ***"
    if len(seq) == 1:
        yield seq
    else:
        for element in permutations([x for x in seq if x != seq[0]]):
            for k in range(len(element) + 1):
                yield element[:k] + [seq[0]] + element[k:]
```











