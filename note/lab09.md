## Recursion and Tree Recursion

### Q2: Subsequences（不会）

A subsequence of a sequence `S` is a sequence of elements from `S`, in the same order they appear in `S`, but possibly with elements missing. Thus, the lists `[]`, `[1, 3]`, `[2]`, and `[1, 2, 3]` are some (but not all) of the subsequences of `[1, 2, 3]`. Write a function that takes a list and returns a list of lists, for which each individual list is a subsequence of the original input.

In order to accomplish this, you might first want to write a function `insert_into_all` that takes an item and a list of lists, adds the item to the beginning of nested list, and returns the resulting list.

```
def insert_into_all(item, nested_list):
    """Assuming that nested_list is a list of lists, return a new list
    consisting of all the lists in nested_list, but with item added to
    the front of each.

    >>> nl = [[], [1, 2], [3]]
    >>> insert_into_all(0, nl)
    [[0], [0, 1, 2], [0, 3]]
    """
    return   [[item]+i for i in nested_list]

def subseqs(s):
    """Assuming that S is a list, return a nested list of all subsequences
    of S (a list of lists). The subsequences can appear in any order.

    >>> seqs = subseqs([1, 2, 3])
    >>> sorted(seqs)
    [[], [1], [1, 2], [1, 2, 3], [1, 3], [2], [2, 3], [3]]
    >>> subseqs([])
    [[]]
    """
    if len(s)<=1:
        return [[],s] if len(s)==1 else [[]]
    else:
        return insert_into_all(s[0],subseqs(s[1:]))+subseqs(s[1:])
```





### Q3: Increasing Subsequences

Just like the last question, we want to write a function that takes a list and returns a list of lists, where each individual list is a subsequence of the original input.

This time we have another condition: we only want the subsequences for which consecutive elements are *nondecreasing*. For example, is a subsequence of , but since 2 < 3, this subsequence would *not* be included in our result.`[1, 3, 2]``[1, 3, 2, 4]`

**Fill in the blanks** to complete the implementation of the function. You may assume that the input list contains no negative elements.`inc_subseqs`

You may use the provided helper function , which takes in an and a list of lists and inserts the to the front of each list.`insert_into_all``item``item`

解析：

这题的思路跟Q2大体类似，但是需要过滤掉一些不符合规则的子集。Q3在里面弄一个辅助函数，多传入一个参数prev用来记录前一个传入的值。当后面遇到的值大于传入的值时，就递归跳过该值。当为正常情况时，直接传入该值并递归调用加上未传入该值递归调用函数返回的值

```
def inc_subseqs(s):
    """Assuming that S is a list, return a nested list of all subsequences
    of S (a list of lists) for which the elements of the subsequence
    are strictly nondecreasing. The subsequences can appear in any order.

    >>> seqs = inc_subseqs([1, 3, 2])
    >>> sorted(seqs)
    [[], [1], [1, 2], [1, 3], [2], [3]]
    >>> inc_subseqs([])
    [[]]
    >>> seqs2 = inc_subseqs([1, 1, 2])
    >>> sorted(seqs2)
    [[], [1], [1], [1, 1], [1, 1, 2], [1, 2], [1, 2], [2]]
    """
    def subseq_helper(s, prev):
        if not s:
            return [[]]
        elif s[0] < prev:
            return subseq_helper(s[1:],prev)
        else:
            a = subseq_helper(s[1:],prev)
            b = subseq_helper(s[1:],s[0])
            return insert_into_all(s[0],b)+a
    return subseq_helper(s,0)
```





### Q4: Number of Trees

A **full binary tree** is a tree where each node has either 2 branches or 0 branches, but never 1 branch.

How many possible full binary tree structures exist that have exactly n leaves?

For those interested in combinatorics, this problem does have a [closed form solution](http://en.wikipedia.org/wiki/Catalan_number)):

```
    if n==1 or n==2::
        return 1
    return sum(num_trees(i)*num_trees(n-i) for i in range(1,n))
```

每一边至少有1个叶子，因此range里面的end=n





### Q5: Generators generator(不会)

Write the generator function , which takes a zero-argument generator function and returns a generator that yields generators. For each element yielded by the generator object returned by calling , a new generator object is yielded that will generate entries 1 through yielded by the generator returned by .`make_generators_generator``g``e``g``e``g`

```
def make_generators_generator(g):
    """Generates all the "sub"-generators of the generator returned by
    the generator function g.

    >>> def every_m_ints_to(n, m):
    ...     i = 0
    ...     while (i <= n):
    ...         yield i
    ...         i += m
    ...
    >>> def every_3_ints_to_10():
    ...     for item in every_m_ints_to(10, 3):
    ...         yield item
    ...
    >>> for gen in make_generators_generator(every_3_ints_to_10):
    ...     print("Next Generator:")
    ...     for item in gen:
    ...         print(item)
    ...
    Next Generator:
    0
    Next Generator:
    0
    3
    Next Generator:
    0
    3
    6
    Next Generator:
    0
    3
    6
    9
    """
    def gen(i):
        for x in g() :
            if i<=0:
               return
            yield x
            i-=1
    i=1
    for m in g():
        yield gen(i)
        i+=1
```



## Objects

### Q6: Keyboard

We'd like to create a class that takes in an arbitrary number of s and stores these s in a dictionary. The keys in the dictionary will be ints that represent the postition on the , and the values will be the respective . Fill out the methods in the class according to each description, using the doctests as a reference for the behavior of a .`Keyboard``Button``Button``Keyboard``Button``Keyboard``Keyboard`

```
class Keyboard:
    """A Keyboard takes in an arbitrary amount of buttons, and has a
    dictionary of positions as keys, and values as Buttons.

    >>> b1 = Button(0, "H")
    >>> b2 = Button(1, "I")
    >>> k = Keyboard(b1, b2)
    >>> k.buttons[0].key
    'H'
    >>> k.press(1)
    'I'
    >>> k.press(2) #No button at this position
    ''
    >>> k.typing([0, 1])
    'HI'
    >>> k.typing([1, 0])
    'IH'
    >>> b1.times_pressed
    2
    >>> b2.times_pressed
    3
    """

    def __init__(self, *args):
        self.buttons={}
        for i in args:
           self.buttons[i.pos]=i
    def press(self, info):
        """Takes in a position of the button pressed, and
        returns that button's output"""
        if  info in self.buttons:
            pressed_key=self.buttons[info]
            pressed_key.times_pressed+=1
            return pressed_key.key
        return ''



    def typing(self, typing_input):
        """Takes in a list of positions of buttons pressed, and
        returns the total output"""
        out_put=''
        for i in typing_input:
            out_put+=self.press(i)
        return out_put
```

总结：当使用哈希表时，要使用{}。另外如果要将对象传入进去，那么赋值的时候需要将对象作为值传进去



## Q7: Advanced Counter

Complete the definition of , which creates a function that creates counters. These counters can not only update their personal count, but also a shared count for all counters. They can also reset either count.make_advanced_counter_maker

```
def make_advanced_counter_maker():
    """Makes a function that makes counters that understands the
    messages "count", "global-count", "reset", and "global-reset".
    See the examples below:

    >>> make_counter = make_advanced_counter_maker()
    >>> tom_counter = make_counter()
    >>> tom_counter('count')
    1
    >>> tom_counter('count')
    2
    >>> tom_counter('global-count')
    1
    >>> jon_counter = make_counter()
    >>> jon_counter('global-count')
    2
    >>> jon_counter('count')
    1
    >>> jon_counter('reset')
    >>> jon_counter('count')
    1
    >>> tom_counter('count')
    3
    >>> jon_counter('global-count')
    3
    >>> jon_counter('global-reset')
    >>> tom_counter('global-count')
    1
    """
    global_count=0
    def counter_maker():
        nonlocal global_count
        count=0
        def counter(n):
            nonlocal count,global_count
            if n=="count":
                count+=1
                return count
            elif n=="global-count":
                global_count+=1
                return global_count
            elif n=="reset":
                count=0
            elif n=='global-reset':
                global_count=0
        return counter
    return counter_maker
    "*** YOUR CODE HERE ***"
    # as many lines as you want
```





# Mutable Lists

## Q8: Trade

In the integer market, each participant has a list of positive integers to trade. When two participants meet, they trade the smallest non-empty prefix of their list of integers. A prefix is a slice that starts at index 0.

Write a function that exchanges the first elements of list with the first elements of list , such that the sums of those elements are equal, and the sum is as small as possible. If no such prefix exists, return the string and do not change either list. Otherwise change both lists and return . A partial implementation is provided.trademfirstnsecond'No deal!''Deal!'

```
def trade(first, second):
    """Exchange the smallest prefixes of first and second that have equal sum.

    >>> a = [1, 1, 3, 2, 1, 1, 4]
    >>> b = [4, 3, 2, 7]
    >>> trade(a, b) # Trades 1+1+3+2=7 for 4+3=7
    'Deal!'
    >>> a
    [4, 3, 1, 1, 4]
    >>> b
    [1, 1, 3, 2, 2, 7]
    >>> c = [3, 3, 2, 4, 1]
    >>> trade(b, c)
    'No deal!'
    >>> b
    [1, 1, 3, 2, 2, 7]
    >>> c
    [3, 3, 2, 4, 1]
    >>> trade(a, c)
    'Deal!'
    >>> a
    [3, 3, 2, 1, 4]
    >>> b
    [1, 1, 3, 2, 2, 7]
    >>> c
    [4, 3, 1, 4, 1]
    """
    m, n = 1, 1

    equal_prefix = lambda: sum(first[:m])-sum((second[:n]))
    while equal_prefix()!=0 and m<len(first) and n<len(second):
        if equal_prefix()<0:
            m += 1
        else:
            n += 1

    if not equal_prefix():
        first[:m], second[:n] = second[:n], first[:m]
        return 'Deal!'
    else:
        return 'No deal!'
```

知识点：

```
dict.get(a,b)  ,在dict中搜寻key=a并返回value，若是不存在，则返回b
```



## Q9(题目看不懂。。。)







## Linked Lists

### Q10: Insert

Implement a function `insert` that takes a `Link`, a `value`, and an `index`, and inserts the `value` into the `Link` at the given `index`. You can assume the linked list already has at least one element. Do not return anything -- `insert` should mutate the linked list.

```
def insert(link, value, index):
    """Insert a value into a Link at the given index.

    >>> link = Link(1, Link(2, Link(3)))
    >>> print(link)
    <1 2 3>
    >>> insert(link, 9001, 0)
    >>> print(link)
    <9001 1 2 3>
    >>> insert(link, 100, 2)
    >>> print(link)
    <9001 1 100 2 3>
    >>> insert(link, 4, 5)
    IndexError
    """
    if index == 0:
        link.rest=Link(link.first,link.rest)
        link.first=value
    elif link.rest == Link.empty :
        raise IndexError
    else:
        insert(link.rest,value,index-1)
```

知识点：

```
raise
```





### Q11: Deep Linked List Length

A linked list that contains one or more linked lists as elements is called a *deep* linked list. Write a function that takes in a (possibly deep) linked list and returns the *deep length* of that linked list. The deep length of a linked list is the total number of non-link elements in the list, as well as the total number of elements contained in all contained lists. See the function's doctests for examples of the deep length of linked lists.`deep_len`



```
  if lnk is Link.empty:
        return 0
    elif not isinstance(lnk,Link):
        return 1
    else:
        return deep_len(lnk.first)+deep_len(lnk.rest)
```

```
isinstance(object,class)，判断object 是否是 class
```





### Q12: Linked Lists as Strings(递归)

Kevin and Jerry like different ways of displaying the linked list structure in Python. While Kevin likes box and pointer diagrams, Jerry prefers a more futuristic way. Write a function that returns a function that converts the linked list to a string in their preferred style.`make_to_string`

*Hint*: You can convert numbers to strings using the function, and you can combine strings together using .`str``+`

```
def deep_len(lnk):
    """ Returns the deep length of a possibly deep linked list.

    >>> deep_len(Link(1, Link(2, Link(3))))
    3
    >>> deep_len(Link(Link(1, Link(2)), Link(3, Link(4))))
    4
    >>> levels = Link(Link(Link(1, Link(2)), \
            Link(3)), Link(Link(4), Link(5)))
    >>> print(levels)
    <<<1 2> 3> <4> 5>
    >>> deep_len(levels)
    5
    """
    if lnk is Link.empty:
        return 0
    elif not isinstance(lnk,Link):
        return 1
    else:
        return deep_len(lnk.first)+deep_len(lnk.rest)
```





### Q13: Prune Small

Complete the function that takes in a and a number and prunes mutatively. If or any of its branches has more than branches, the branches with the smallest labels should be kept and any other branches should be *pruned*, or removed, from the tree.`prune_small``Tree``t``n``t``t``n``n`

```
def prune_small(t, n):
    """Prune the tree mutatively, keeping only the n branches
    of each node with the smallest label.

    >>> t1 = Tree(6)
    >>> prune_small(t1, 2)
    >>> t1
    Tree(6)
    >>> t2 = Tree(6, [Tree(3), Tree(4)])
    >>> prune_small(t2, 1)
    >>> t2
    Tree(6, [Tree(3)])
    >>> t3 = Tree(6, [Tree(1), Tree(3, [Tree(1), Tree(2), Tree(3)]), Tree(5, [Tree(3), Tree(4)])])
    >>> prune_small(t3, 2)
    >>> t3
    Tree(6, [Tree(1), Tree(3, [Tree(1), Tree(2)])])
    """
    while not len(t.branches)<=n:
        largest = max(t.branches, key=lambda x:x.label)
        t.branches=[x for x in t.branches if x is not largest]
    for i in t.branches:
        prune_small(i,n)
```







