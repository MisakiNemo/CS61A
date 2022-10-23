

# Mutible Function

![image-20221012220336370](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012220336370.png)

知识点：

```
nonlocal，就是在当前框架之外去搜寻参数，并使用框架之外的参数
```

**实际上就是将nonlocal修饰的变量与非本地框架（往外的框架寻找）中的同名变量绑定，这样当当前变量修改时，外边的同名变量也会修改。又因为高阶函数的框架实际上是会一直存在的，因此就会有上面的情形**



# Nonlocal Function

## The Effect of Nonlocal Statements

![image-20221012221630258](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012221630258.png)

将nonlocal修饰的变量名与非本地框架的变量（外面的框架）中的同名变量绑定起来。

**condition**：

**当前框架中不能预先声明同名的变量**

**非本地框架中必须存在同名变量**



## The Many Meanings of Assignment Statements

![image-20221012223247206](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012223247206.png)

![image-20221012223650459](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012223650459.png)





## Mutable Values & Persistent Local State  

![image-20221012224112140](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012224112140.png)

**实际上可以理解成在父框架创建一个指针，然后在里面的框架调用这个指针并修改指针指向的值**





# Multiple Mutable Function

![image-20221012225359947](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012225359947.png)

虽然返回的值相同，但是它们并不互相影响，因为它们在不同的框架（环境）中运行。







# Lab 6: Nonlocal, Mutability

### Q1: Make Adder Increasing

Write a function which takes in an integer `a` and returns a one-argument function. This function should take in some value `b` and return `a + b` the first time it is called, similar to `make_adder`. The second time it is called, however, it should return `a + b + 1`, then `a + b + 2` the third time, and so on.

### code

```
def make_adder_inc(a):
    """
    >>> adder1 = make_adder_inc(5)
    >>> adder2 = make_adder_inc(6)
    >>> adder1(2)
    7
    >>> adder1(2) # 5 + 2 + 1
    8
    >>> adder1(10) # 5 + 10 + 2
    17
    >>> [adder1(x) for x in [1, 2, 3]]
    [9, 11, 13]
    >>> adder2(5)
    11
    """
    "*** YOUR CODE HERE ***"
     x=-1
    def func(b):
        nonlocal x
        x=x+1
        return a+b+x
    return func
```



## Q2: Next Fibonacci

Write a function `make_fib` that returns a function that returns the next Fibonacci number each time it is called. (The Fibonacci sequence begins with 0 and then 1, after which each element is the sum of the preceding two.) Use a `nonlocal` statement! In addition, do not use python lists to solve this problem.

### code

```
def make_fib():
    """Returns a function that returns the next Fibonacci number
    every time it is called.

    >>> fib = make_fib()
    >>> fib()
    0
    >>> fib()
    1
    >>> fib()
    1
    >>> fib()
    2
    >>> fib()
    3
    >>> fib2 = make_fib()
    >>> fib() + sum([fib2() for _ in range(5)])
    12
    >>> from construct_check import check
    >>> # Do not use lists in your implementation
    >>> check(this_file, 'make_fib', ['List'])
    True
    """
    "*** YOUR CODE HERE ***"
    pre=0
    cur=1
    def func():
        nonlocal pre,cur
        a,b=pre,cur
        pre,cur=b,a+b
        return a
    return func
```







## Q3: List-Mutation

```
List Mutation > Suite 1 > Case 1
(cases remaining: 1)

What would Python display? If you get stuck, try it out in the Python
interpreter!

>>> lst = [5, 6, 7, 8]
>>> lst.append(6)
? [5,7,8]
-- Not quite. Try again! --

? [5,6,7,8,6]
-- Not quite. Try again! --

? [5,6,7,8,6]
-- Not quite. Try again! --

? [5,6,7,8,6]
-- Not quite. Try again! --

? [6,5,6,7,8]
-- Not quite. Try again! --

? 5,6,7,8,6
-- Not quite. Try again! --

? list
-- Not quite. Try again! --

? nothing
-- OK! --

>>> lst
? [5,6,7,8,6]
-- OK! --

>>> lst.insert(0, 9)
>>> lst
? [9,5,6,7,8,6]
-- OK! --

>>> x = lst.pop(2)
>>> lst
? [5,6,8,6]
-- Not quite. Try again! --

? 7
-- Not quite. Try again! --

? [9,5,7,8,6]
-- OK! --

>>> lst.remove(x)
>>> lst
? [9,5,7,8]
-- OK! --

>>> a, b = lst, lst[:]
>>> a is lst
? True
-- OK! --

>>> b == lst
? True
-- OK! --

>>> b is lst
? True
-- Not quite. Try again! --

? False
-- OK! --

```





## Q4: Insert Items

Write a function which takes in a list `lst`, an argument `entry`, and another argument `elem`. This function will check through each item present in `lst` to see if it is equivalent with `entry`. Upon finding an equivalent entry, the function should modify the list by placing `elem` into the list right after the found entry. At the end of the function, the modified list should be returned. See the doctests for examples on how this function is utilized. Use list mutation to modify the original list, no new lists should be created or returned.

**Be careful in situations where the values passed into `entry` and `elem` are equivalent, so as not to create an infinitely long list while iterating through it.** If you find that your code is taking more than a few seconds to run, it is most likely that the function is in a loop of inserting new values.

### code

```
def insert_items(lst, entry, elem):
    """
    >>> test_lst = [1, 5, 8, 5, 2, 3]
    >>> new_lst = insert_items(test_lst, 5, 7)
    >>> new_lst
    [1, 5, 7, 8, 5, 7, 2, 3]
    >>> large_lst = [1, 4, 8]
    >>> large_lst2 = insert_items(large_lst, 4, 4)
    >>> large_lst2
    [1, 4, 4, 8]
    >>> large_lst3 = insert_items(large_lst2, 4, 6)
    >>> large_lst3
    [1, 4, 6, 4, 6, 8]
    >>> large_lst3 is large_lst
    True
    """
    "*** YOUR CODE HERE ***"
    index=[i for i in range(len(lst)) if lst[i]==entry]
    for i in range(len(index)):
        lst[index[i]+i+1:]=[elem]+lst[index[i]+i+1:]
    return lst
```

