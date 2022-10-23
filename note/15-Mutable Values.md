# Object

**对象可以调用封装的函数**<img src="C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221011230826718.png" alt="image-20221011230826718" style="zoom: 50%;" />

<img src="C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221011230858281.png" alt="image-20221011230858281" style="zoom:50%;" />





## Example String

```
str.upper()
str.lower()
str.swapcase()
```



#### ASCII Standard

lookup(表情包)

name()返回字符的ASCII值



# Multation operation

<img src="C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221011235748386.png" alt="image-20221011235748386" style="zoom:50%;" />

我感觉是相当于指针

![image-20221012085253931](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012085253931.png)

确实是指针，list，容器等一系列抽象数据类型的变量名是都是一个指针





# Tuples

实际上是一个不可变的序列

![image-20221012090918099](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012090918099.png)

tuple里面的值是不可变的，但是若tuple里面传入的是list等的数据类型，即传入的是一个指针，不可以改变指针指向，但是可以通过指针改变指针指向的列表的数据







# Mutation

![image-20221012093643061](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012093643061.png)

每个函数的默认变量值都是一个固定的参数（指针/地址），若是该指向的地址包含的数据改变，那么函数调用的参数也会发生改变。







# Example :Lists

![image-20221012102137622](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012102137622.png)

![image-20221012102151076](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012102151076.png)

![image-20221012102918746](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012102918746.png)

![image-20221012104610551](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012104610551.png)

##### **知识点**

**这里第一个例子中间多出一个指针，是因为t[1:2]本身返回的是一个一维列表，而[1:2]之间的元素本事就是一个列表，因此返回的是一个二维列表，因此中间就多出了一个指针。**







# HW03（Q7之后的一些是检测你的对抽象数据的理解的，不写了0.0）

#### 前置代码

##### C1

```
def min_depth(t):
    """A simple function to return the distance between t's root and its closest leaf"""
    if is_leaf(t):
        return 0
    h = float('inf')
    for b in branches(t):
        # Still works fine!""" if is_leaf(b): return 1"""     这一行是多余的，因为实际上下一行已经把这种情况包含了
        h = min(h, 1 + min_depth(b))
    return h
```

```
无穷大：float('inf')       infinnity
```





## Q1

![image-20221012124553656](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012124553656.png)

```
def mobile(left, right):
    """Construct a mobile from a left arm and a right arm."""
    assert is_arm(left), "left must be a arm"
    assert is_arm(right), "right must be a arm"
    return ['mobile', left, right]

def is_mobile(m):
    """Return whether m is a mobile."""
    return type(m) == list and len(m) == 3 and m[0] == 'mobile'

def left(m):
    """Select the left arm of a mobile."""
    assert is_mobile(m), "must call left on a mobile"
    return m[1]

def right(m):
    """Select the right arm of a mobile."""
    assert is_mobile(m), "must call right on a mobile"
    return m[2]

def arm(length, mobile_or_planet):
    """Construct a arm: a length of rod with a mobile or planet at the end."""
    assert is_mobile(mobile_or_planet) or is_planet(mobile_or_planet)
    return ['arm', length, mobile_or_planet]

def is_arm(s):
    """Return whether s is a arm."""
    return type(s) == list and len(s) == 3 and s[0] == 'arm'

def length(s):
    """Select the length of a arm."""
    assert is_arm(s), "must call length on a arm"
    return s[1]

def end(s):
    """Select the mobile or planet hanging at the end of a arm."""
    assert is_arm(s), "must call end on a arm"
    return s[2]

def planet(size):
    """Construct a planet of some size."""
    assert size > 0
    "*** YOUR CODE HERE ***"
    return ['planet',size]

def size(w):
    """Select the size of a planet."""
    assert is_planet(w), 'must call size on a planet'
    "*** YOUR CODE HERE ***"
    return w[1]

def is_planet(w):
    """Whether w is a planet."""
    return type(w) == list and len(w) == 2 and w[0] == 'planet'

def examples():
    t = mobile(arm(1, planet(2)),
               arm(2, planet(1)))
    u = mobile(arm(5, planet(1)),
               arm(1, mobile(arm(2, planet(3)),
                              arm(3, planet(2)))))
    v = mobile(arm(4, t), arm(2, u))
    return (t, u, v)

def total_weight(m):
    """Return the total weight of m, a planet or mobile.

    >>> t, u, v = examples()
    >>> total_weight(t)
    3
    >>> total_weight(u)
    6
    >>> total_weight(v)
    9
    >>> from construct_check import check
    >>> # checking for abstraction barrier violations by banning indexing
    >>> check(HW_SOURCE_FILE, 'total_weight', ['Index'])
    True
    """
    if is_planet(m):
        return size(m)
    else:
        assert is_mobile(m), "must get total weight of a mobile or a planet"
        return total_weight(end(left(m))) + total_weight(end(right(m)))
```

看一下代码就好，感觉跟树大差不差，但确实感觉是构成了一个系统结构

## Q2

![image-20221012190706366](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012190706366.png)

### code

```
def balanced(m):
    """Return whether m is balanced.

    >>> t, u, v = examples()
    >>> balanced(t)
    True
    >>> balanced(v)
    True
    >>> w = mobile(arm(3, t), arm(2, u))
    >>> balanced(w)
    False
    >>> balanced(mobile(arm(1, v), arm(1, w)))
    False
    >>> balanced(mobile(arm(1, w), arm(1, v)))
    False
    >>> from construct_check import check
    >>> # checking for abstraction barrier violations by banning indexing
    >>> check(HW_SOURCE_FILE, 'balanced', ['Index'])
    True
    """
    "*** YOUR CODE HERE ***"
    if is_planet(m):
        return True
    else:
        return length(left(m))*total_weight(end(left(m)))==length(right(m))*total_weight(end(right(m))) and balanced(end(left(m))) and balanced(end(right(m)))
        
```





## Q3

![image-20221012190747221](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221012190747221.png)

### code

```
 """Return a tree representing the mobile with its total weight at the root.

    >>> t, u, v = examples()
    >>> print_tree(totals_tree(t))
    2
      1
      0
    >>> print_tree(totals_tree(u))
    5
      0
      4
        2
        1
    >>> print_tree(totals_tree(v))
    8
      2
        1
        0
      5
        0
        4
          2
          1
    >>> from construct_check import check
    >>> # checking for abstraction barrier violations by banning indexing
    >>> check(HW_SOURCE_FILE, 'totals_tree', ['Index'])
    True
    """
    "*** YOUR CODE HERE ***"
    if is_planet(m):
        return tree(size(m))
    else:
        l=totals_tree(end(left(m)))
        r=totals_tree(end(right(m)))
        return tree(total_weight(m),[l,r])
```





### Q4: Replace Leaf

Define `replace_leaf`, which takes a tree `t`, a value `find_value`, and a value `replace_value`. `replace_leaf` returns a new tree that's the same as `t` except that every leaf label equal to `find_value` has been replaced with `replace_value`.

### code

```
def replace_leaf(t, find_value, replace_value):
    """Returns a new tree where every leaf value equal to find_value has
    been replaced with replace_value.

    >>> yggdrasil = tree('odin',
    ...                  [tree('balder',
    ...                        [tree('thor'),
    ...                         tree('freya')]),
    ...                   tree('frigg',
    ...                        [tree('thor')]),
    ...                   tree('thor',
    ...                        [tree('sif'),
    ...                         tree('thor')]),
    ...                   tree('thor')])
    >>> laerad = copy_tree(yggdrasil) # copy yggdrasil for testing purposes
    >>> print_tree(replace_leaf(yggdrasil, 'thor', 'freya'))
    odin
      balder
        freya
        freya
      frigg
        freya
      thor
        sif
        freya
      freya
    >>> laerad == yggdrasil # Make sure original tree is unmodified
    True
    """
    "*** YOUR CODE HERE ***"
    if is_leaf(t):
        return tree(replace_value if label(t)==find_value else label(t))
    else:
        s=[replace_leaf(b,find_value,replace_value) for  b in branches(t)]
        return tree(label(t),s)
```

##### 知识点

一个节点的树枝有多个，因此需要使用遍历



## Q5: Preorder(前序遍历)

Define the function `preorder`, which takes in a tree as an argument and returns a list of all the entries in the tree in the order that `print_tree` would print them.

The following diagram shows the order that the nodes would get printed, with the arrows representing function calls.

<img src="https://inst.eecs.berkeley.edu/~cs61a/fa20/hw/hw03/assets/preorder.png" alt="preorder" style="zoom:50%;" />

### code（可以去看一下别人的代码，感觉自己写的不是很好）

```
def preorder(t):
    """Return a list of the entries in this tree in the order that they
    would be visited by a preorder traversal (see problem description).

    >>> numbers = tree(1, [tree(2), tree(3, [tree(4), tree(5)]), tree(6, [tree(7)])])
    >>> preorder(numbers)
    [1, 2, 3, 4, 5, 6, 7]
    >>> preorder(tree(2, [tree(4, [tree(6)])]))
    [2, 4, 6]
    """
    "*** YOUR CODE HERE ***"

    if t==[]:
       return
    else:
         result=[]
         result.append(label(t))
         s=[preorder(b) for b in branches(t)]
         for i in range(len(s)):
             result+=s[i]
         return result
```





## Q6: Has Path

Write a function that takes in a tree and a string . It returns if there is a path that starts from the root where the entries along the path spell out the , and otherwise. (This data structure is called a trie, and it has a lot of cool applications!---think autocomplete). You may assume that every node's is exactly one character.`has_path``t``word``True``word``False``label`

### code

```
def has_path(t, word):
    """Return whether there is a path in a tree where the entries along the path
    spell out a particular word.

    >>> greetings = tree('h', [tree('i'),
    ...                        tree('e', [tree('l', [tree('l', [tree('o')])]),
    ...                                   tree('y')])])
    >>> print_tree(greetings)
    h
      i
      e
        l
          l
            o
        y
    >>> has_path(greetings, 'h')
    True
    >>> has_path(greetings, 'i')
    False
    >>> has_path(greetings, 'hi')
    True
    >>> has_path(greetings, 'hello')
    True
    >>> has_path(greetings, 'hey')
    True
    >>> has_path(greetings, 'bye')
    False
    """
    assert len(word) > 0, 'no path for empty word.'
    
    
    "*** YOUR CODE HERE ***"
    if label(t)==word:
        return True
    elif label(t)==word[0]:
        for b in branches(t):
            if has_path(b,word[1:]):
                return True
    return False
```





## Q7: Interval Abstraction

Alyssa's program is incomplete because she has not specified the implementation of the interval abstraction. She has implemented the constructor for you; fill in the implementation of the selectors.

### code

```
def mul_interval(x, y):
    """Return the interval that contains the product of any value in x and any
    value in y."""
    p1 = lower_bound(x)*lower_bound(y)
    p2 = lower_bound(x)*upper_bound(y)
    p3 = upper_bound(x)*lower_bound(y)
    p4 = upper_bound(x)*upper_bound(y)
    return interval(min(p1, p2, p3, p4), max(p1, p2, p3, p4))
```

#### 知识点

##### format函数

```
>>>"{} {}".format("hello", "world")    # 不设置指定位置，按默认顺序
'hello world'
 
>>> "{0} {1}".format("hello", "world")  # 设置指定位置
'hello world'
 
>>> "{1} {0} {1}".format("hello", "world")  # 设置指定位置
'world hello world'
```

**要注意抽象数据之间的运算获取参数的方式以及返回值的类型和**





## Q8: Sub Interval

Using reasoning analogous to Alyssa's, define a subtraction function for intervals. Try to reuse functions that have already been implemented if you find yourself repeating code.

### code

```
def sub_interval(x, y):
    """Return the interval that contains the difference between any value in x
    and any value in y."""
    "*** YOUR CODE HERE ***"
    return interval(lower_bound(x)-upper_bound(y),upper_bound(x)-lower_bound(y))
```

