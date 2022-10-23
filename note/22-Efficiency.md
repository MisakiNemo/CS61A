# Measuring Efficiency

![image-20221018181510110](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018181510110.png)

高阶函数count返回的是一个函数，该函数的返回值是f(n)，即斐波那契数列n对应的值。但是在返回之前，多进行了一步计数的操作。





# Memorization

![image-20221018183031061](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018183031061.png)

高阶函数的记忆函数





# Exponentiation

![image-20221018190002203](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018190002203.png)





# Orders of Growth

## Quadratic Time

![image-20221018191034968](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018191034968.png)

n^2，

## Common Orders of Growth（各种复杂度）

![image-20221018191012556](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018191012556.png)

从上往下依次为：指数级，平方级，线性级，对数级，恒定值





# Order of Growth Notation

![image-20221018191644855](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018191644855.png)





# Space

![image-20221018192740562](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018192740562.png)

计算同一时间有多少个环境（函数框架）打开







# Lab 8: Linked Lists, Trees

### Q2: Convert Link

Write a function that takes in a linked list and returns the sequence as a Python list. You may assume that the input list is shallow; none of the elements is another linked list.`convert_link`

Try to find both an iterative and recursive solution for this problem!

#### code

```
def convert_link(link):
    """Takes a linked list and returns a Python list with the same elements.

    >>> link = Link(1, Link(2, Link(3, Link(4))))
    >>> convert_link(link)
    [1, 2, 3, 4]
    >>> convert_link(Link.empty)
    []
    """
    "*** YOUR CODE HERE ***"
    res=[]
    while not link == Link.empty:
        res+=[link.first]
        link=link.rest
    return res
```





### Q3: Every Other(不会)

Implement , which takes a linked list . It mutates such that all of the odd-indexed elements (using 0-based indexing) are removed from the list. For example:`every_other``s``s`

#### code

```
def every_other(s):
    """Mutates a linked list so that all the odd-indiced elements are removed
    (using 0-based indexing).

    >>> s = Link(1, Link(2, Link(3, Link(4))))
    >>> every_other(s)
    >>> s
    Link(1, Link(3))
    >>> odd_length = Link(5, Link(3, Link(1)))
    >>> every_other(odd_length)
    >>> odd_length
    Link(5, Link(1))
    >>> singleton = Link(4)
    >>> every_other(singleton)
    >>> singleton
    Link(4)
    """
    "*** YOUR CODE HERE ***"
    if s.rest!=Link.empty and s.rest.rest!=Link.empty:
        s.rest=s.rest.rest
        every_other(s.rest)
    elif s.rest!=Link.empty and s.rest.rest==Link.empty:
        s.rest=Link.empty
```







### Q4: Cumulative Mul

Write a function that mutates the Tree so that each node's label becomes the product of all labels in the subtree rooted at the node.`cumulative_mul``t`

#### code

```
def cumulative_mul(t):
    """Mutates t so that each node's label becomes the product of all labels in
    the corresponding subtree rooted at t.

    >>> t = Tree(1, [Tree(3, [Tree(5)]), Tree(7)])
    >>> cumulative_mul(t)
    >>> t
    Tree(105, [Tree(15, [Tree(5)]), Tree(7)])
    """
    "*** YOUR CODE HERE ***"
    if t.is_leaf():
        return  t.label
    else:
       for b in t.branches:
            cumulative_mul(b)
            t.label*=b.label
```





### Q5: Cycles(不会)

The `Link` class can represent lists with cycles. That is, a list may contain itself as a sublist.

#### code

```
def has_cycle_constant(link):
    """Return whether link contains a cycle.

    >>> s = Link(1, Link(2, Link(3)))
    >>> s.rest.rest.rest = s
    >>> has_cycle_constant(s)
    True
    >>> t = Link(1, Link(2, Link(3)))
    >>> has_cycle_constant(t)
    False
    """
    "*** YOUR CODE HERE ***"
    p_slow, p_fast = link, link
    while p_fast != Link.empty:
        p_slow = p_slow.rest
        if p_fast.rest != Link.empty:
            p_fast = p_fast.rest.rest
            if p_slow == p_fast:
                return True
        else:
            break
```





### Q6: Reverse Other(真的不会啊啊啊啊啊啊啊！！！)

Write a function `reverse_other` that mutates the tree such that **labels** on *every other* (odd-depth) level are reversed. For example, `Tree(1,[Tree(2, [Tree(4)]), Tree(3)])` becomes `Tree(1,[Tree(3, [Tree(4)]), Tree(2)])`. Notice that the nodes themselves are *not* reversed; only the labels are.

#### code

```

```

