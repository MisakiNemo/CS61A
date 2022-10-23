# Linked List

![image-20221018150433845](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018150433845.png)

![image-20221018150459506](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018150459506.png)





# Linked List Processing

![image-20221018151508102](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018151508102.png)

![image-20221018151442548](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018151442548.png)





# Linked List Mutation

![image-20221018152135251](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018152135251.png)

实际上是一个循环链表，在5和2之中循环





# Linked List Mutation Example

![image-20221018153014441](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018153014441.png)





# Tree Class

![image-20221018154419566](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018154419566.png)

![image-20221018154446547](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018154446547.png)





# Tree Mutation

![image-20221018154615124](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018154615124.png)







# Homework 5: Object-Oriented Programming, Linked Lists, Trees

## OOP

### Q1: Vending Machine

Create a class called `VendingMachine` that represents a vending machine for some product. A `VendingMachine` object returns strings describing its interactions.

Fill in the `VendingMachine` class, adding attributes and methods as appropriate, such that its behavior matches the following doctests:

### code

```
class VendingMachine:
    """A vending machine that vends some product for some price.

    >>> v = VendingMachine('candy', 10)
    >>> v.vend()
    'Inventory empty. Restocking required.'
    >>> v.add_funds(15)
    'Inventory empty. Restocking required. Here is your $15.'
    >>> v.restock(2)
    'Current candy stock: 2'
    >>> v.vend()
    'You must add $10 more funds.'
    >>> v.add_funds(7)
    'Current balance: $7'
    >>> v.vend()
    'You must add $3 more funds.'
    >>> v.add_funds(5)
    'Current balance: $12'
    >>> v.vend()
    'Here is your candy and $2 change.'
    >>> v.add_funds(10)
    'Current balance: $10'
    >>> v.vend()
    'Here is your candy.'
    >>> v.add_funds(15)
    'Inventory empty. Restocking required. Here is your $15.'

    >>> w = VendingMachine('soda', 2)
    >>> w.restock(3)
    'Current soda stock: 3'
    >>> w.restock(3)
    'Current soda stock: 6'
    >>> w.add_funds(2)
    'Current balance: $2'
    >>> w.vend()
    'Here is your soda.'
    """
    "*** YOUR CODE HERE ***"
    def __init__(self,name,price):
        self.name=name
        self.price=price
        self.stock=0
        self.funds=0
    def add_funds(self,funds):
        if self.stock==0:
            return 'Inventory empty. Restocking required. Here is your ${0}.'.format(funds)
        self.funds+=funds
        return 'Current balance: ${0}'.format(self.funds)
    def restock(self,num):
       self.stock+=num
       return 'Current {1} stock: {0}'.format(self.stock,self.name)
    def vend(self):
       if self.stock==0:
           return 'Inventory empty. Restocking required.'
       if self.funds<self.price:
           return 'You must add ${0} more funds.'.format(self.price-self.funds)
       else:
           tmp=self.funds-self.price
           self.funds=0
           self.stock-=1
           return 'Here is your {0}.'.format(self.name) if tmp==0 else 'Here is your {1} and ${0} change.'.format(tmp,self.name)
```



------



### Q2: Mint

Complete the `Mint` and `Coin` classes so that the coins created by a mint have the correct year and worth.

- Each `Mint` instance has a `year` stamp. The `update` method sets the `year` stamp to the `current_year` class attribute of the `Mint` class.
- The `create` method takes a subclass of `Coin` and returns an instance of that class stamped with the `mint`'s year (which may be different from `Mint.current_year` if it has not been updated.)
- A `Coin`'s `worth` method returns the `cents` value of the coin plus one extra cent for each year of age beyond 50. A coin's age can be determined by subtracting the coin's year from the `current_year` class attribute of the `Mint` class.

#### code

```
class Mint:
    """A mint creates coins by stamping on years.

    The update method sets the mint's stamp to Mint.current_year.

    >>> mint = Mint()
    >>> mint.year
    2020
    >>> dime = mint.create(Dime)
    >>> dime.year
    2020
    >>> Mint.current_year = 2100  # Time passes
    >>> nickel = mint.create(Nickel)
    >>> nickel.year     # The mint has not updated its stamp yet
    2020
    >>> nickel.worth()  # 5 cents + (80 - 50 years)
    35
    >>> mint.update()   # The mint's year is updated to 2100
    >>> Mint.current_year = 2175     # More time passes
    >>> mint.create(Dime).worth()    # 10 cents + (75 - 50 years)
    35
    >>> Mint().create(Dime).worth()  # A new mint has the current year
    10
    >>> dime.worth()     # 10 cents + (155 - 50 years)
    115
    >>> Dime.cents = 20  # Upgrade all dimes!
    >>> dime.worth()     # 20 cents + (155 - 50 years)
    125
    """
    current_year = 2020

    def __init__(self):
        self.update()
        self.year=Mint.current_year

    def create(self, kind):
        "*** YOUR CODE HERE ***"
        return kind(self.current_year)

    def update(self):
        "*** YOUR CODE HERE ***"
        self.current_year=Mint.current_year
class Coin:
    def __init__(self, year):
        self.year = year

    def worth(self):
        "*** YOUR CODE HERE ***"
        return Mint.current_year-self.year-50+self.cents if Mint.current_year-self.year>=50 else self.cents
class Nickel(Coin):
    cents = 5

class Dime(Coin):
    cents = 10
```





## Linked Lists(不会)

### Q3: Store Digits

Write a function `store_digits` that takes in an integer `n` and returns a linked list where each element of the list is a digit of `n`.

#### code

```
def store_digits(n):
    """Stores the digits of a positive number n in a linked list.

    >>> s = store_digits(1)
    >>> s
    Link(1)
    >>> store_digits(2345)
    Link(2, Link(3, Link(4, Link(5))))
    >>> store_digits(876)
    Link(8, Link(7, Link(6)))
    >>> # a check for restricted functions
    >>> import inspect, re
    >>> cleaned = re.sub(r"#.*\\n", '', re.sub(r'"{3}[\s\S]*?"{3}', '', inspect.getsource(store_digits)))
    >>> print("Do not use str or reversed!") if any([r in cleaned for r in ["str", "reversed"]]) else None
    """
    "*** YOUR CODE HERE ***"
    def helper(lst,n):
        if n==0:
            return lst
        lst=Link(n%10,lst)
        return helper(lst,n//10)
    ans=Link(n%10,Link.empty)
    return helper(ans,n//10)
```





## Trees

### Q4: Is BST(不会)

Write a function `is_bst`, which takes a Tree `t` and returns `True` if, and only if, `t` is a valid binary search tree, which means that:

- Each node has at most two children (a leaf is automatically a valid binary search tree)
- The children are valid binary search trees
- For every node, the entries in that node's left child are less than or equal to the label of the node
- For every node, the entries in that node's right child are greater than the label of the node

An example of a BST is:

![bst](https://miro.medium.com/max/1424/1*F8MmBnUQyOA8-Rajg69nSQ.png)

Note that, if a node has only one child, that child could be considered either the left or right child. You should take this into consideration.

*Hint:* It may be helpful to write helper functions `bst_min` and `bst_max` that return the minimum and maximum, respectively, of a Tree if it is a valid binary search tree.

#### code

```

```





### Q5: Preorder

Define the function `preorder`, which takes in a tree as an argument and returns a list of all the entries in the tree in the order that `print_tree` would print them.

The following diagram shows the order that the nodes would get printed, with the arrows representing function calls.

![preorder](https://inst.eecs.berkeley.edu/~cs61a/fa20/hw/hw05/assets/preorder.png)

#### code

```
def preorder(t):
    """Return a list of the entries in this tree in the order that they
    would be visited by a preorder traversal (see problem description).

    >>> numbers = Tree(1, [Tree(2), Tree(3, [Tree(4), Tree(5)]), Tree(6, [Tree(7)])])
    >>> preorder(numbers)
    [1, 2, 3, 4, 5, 6, 7]
    >>> preorder(Tree(2, [Tree(4, [Tree(6)])]))
    [2, 4, 6]
    """
    "*** YOUR CODE HERE ***"
    num=[]

    def helper(t):
        if t.is_leaf():
            num.append(t.label)
        else:
            num.append(t.label)
            for i in t.branches:
                helper(i)
    helper(t)
    return num
```







## Generators/Trees

### Q6: Yield Paths（记住函数的结果可以作为遍历对象）

Define a generator function `path_yielder` which takes in a Tree `t`, a value `value`, and returns a generator object which yields each path from the root of `t` to a node that has label `value`.

`t` is implemented with a class, not as the function-based ADT.

Each path should be represented as a list of the labels along that path in the tree. You may yield the paths in any order.

We have provided a (partial) skeleton for you. You do not need to use this skeleton, but if your implementation diverges significantly from it, you might want to think about how you can get it to fit the skeleton.

#### code

```
    if t.label==value:
        yield [t.label]
    else:
      for b in t.branches:
        for path in path_yielder(b,value):
          yield [t.label]+path
```

