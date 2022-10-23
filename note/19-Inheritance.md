# Review

![image-20221013172737454](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013172737454.png)

![image-20221013172839575](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013172839575.png)



# Attributes

![image-20221013193519923](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221013193519923.png)

修改类中的属性时直接调用类名，若是为单独一个对象设置特殊的属性，那么就应该使用对象名来调用并赋值或更改

# Attribute Assignment





# Inheritance

![image-20221014080446554](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221014080446554.png)

继承：与父类有相同的属性和方法，但是这些方法可能有所区别以及在父类的属性和方法的基础之上还有其他的一些新的属性和方法。

继承的语法，看图



![image-20221014080825559](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221014080825559.png)

当计算机运行一个.语句时，会先在当前的对象中寻找该属性或者方法，若没有，则在类中寻找；若没有，则到父类中寻找；若没有，则在爷类中寻找......



# Object-Oriented Design

## Inheritance Design（上下继承）

![image-20221014081145992](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221014081145992.png)

当已经在子类中定义了覆盖父类的函数，我们仍然通过调用父类的类名来调用父类中的属性或者方法。通过进一步的创建子类或者创建特殊的对象，来创建一个特殊的账户



## Inheritance and Composition(个体与集合)

![image-20221014082021613](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221014082021613.png)

![image-20221014082601885](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221014082601885.png)





# Attribute Lookup Practice

![image-20221014083001476](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221014083001476.png)



# Multiple Inheritance

多类继承：子类继承多个基类叫多类继承

![image-20221014083449244](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221014083449244.png)

当在当前对象和类中寻找不到属性和方法时，会从最近的父类寻找，循环往复

# Complicated Inheritance

多重继承：会让程序变得非常复杂，尽量少用

![image-20221014083852860](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221014083852860.png)

形象起来了，那个亲戚是我的谁谁谁，另一个又是我的谁谁谁，已经裂开了





# Lab 7: Iterators, Generators, Object-Oriented Programming

## Iterators and Generators

### Q1: Scale

Implement the generator function , which yields elements of the given iterable , scaled by . As an extra challenge, try writing this function using a statement!`scale(it, multiplier)``it``multiplier``yield from`

ad：只使用上面几个参数的方法不会- -

#### code

```
def scale(it, multiplier):
    """Yield elements of the iterable it scaled by a number multiplier.

    >>> m = scale([1, 5, 2], 5)
    >>> type(m)
    <class 'generator'>
    >>> list(m)
    [5, 25, 10]

    >>> m = scale(naturals(), 2)
    >>> [next(m) for _ in range(5)]
    [2, 4, 6, 8, 10]
    """
    "*** YOUR CODE HERE ***"
    for i in  iter(it):
        yield multiplier*i
```

##### plus code

```
yield from map(lambda x:multiplier*x,it)
```





### Q2: Hailstone

Write a generator that outputs the hailstone sequence from homework 1.

Here's a quick reminder of how the hailstone sequence is defined:

1. Pick a positive integer as the start.`n`
2. If is even, divide it by 2.`n`
3. If is odd, multiply it by 3 and add 1.`n`
4. Continue this process until is 1.`n`

**Note:** It is highly encouraged (though not required) to try writing a solution using recursion for some extra practice. Since returns a generator, you can a call to !`hailstone``yield from``hailstone`

#### code

```
def hailstone(n):
    """
    >>> for num in hailstone(10):
    ...     print(num)
    ...
    10
    5
    16
    8
    4
    2
    1
    """
    "*** YOUR CODE HERE ***"
        while not n==1:
          yield n
          if n%2==0:
            n//=2
          else:
            n=n*3+1
        yield 1
```

##### plus code(recursive)

```
    if n==1:
        yield 1
    else:
        yield n
        n=n//2 if n%2==0 else n*3+1
        yield from hailstone(n)
```





## WWPD: Objects

### Q3: The Car class（Q&A）

**Note:** These questions use inheritance. For an overview of inheritance, see the [inheritance portion](http://composingprograms.com/pages/25-object-oriented-programming.html#inheritance) of Composing Programs

Below is the definition of a class that we will be using in the following WWPD questions. **Note:** This definition can also be found in .`Car``car.py`

#### code

```
class Car(object):
    num_wheels = 4
    gas = 30
    headlights = 2
    size = 'Tiny'

    def __init__(self, make, model):
        self.make = make
        self.model = model
        self.color = 'No color yet. You need to paint me.'
        self.wheels = Car.num_wheels
        self.gas = Car.gas

    def paint(self, color):
        self.color = color
        return self.make + ' ' + self.model + ' is now ' + color

    def drive(self):
        if self.wheels < Car.num_wheels or self.gas <= 0:
            return 'Cannot drive!'
        self.gas -= 10
        return self.make + ' ' + self.model + ' goes vroom!'

    def pop_tire(self):
        if self.wheels > 0:
            self.wheels -= 1

    def fill_gas(self):
        self.gas += 20
        return 'Gas level: ' + str(self.gas)
```





### Q4: Making Cards

To play a card game, we're going to need to have cards, so let's make some! We're gonna implement the basics of the class first.`Card`

First, implement the class constructor in . This constructor takes three arguments:`Card``classes.py`

- the of the card, a string`name`
- the stat of the card, an integer`attack`
- the stat of the card, an integer`defense`

Each instance should keep track of these values using instance attributes called , , and .`Card``name``attack``defense`

You should also implement the method in , which takes in another card as an input and calculates the current card's power. Check the Rules section if you want a refresher on how power is calculated.`power``Card`

#### code

```
class Card:
    cardtype = 'Staff'

    def __init__(self, name, attack, defense):
        """
        Create a Card object with a name, attack,
        and defense.
        >>> staff_member = Card('staff', 400, 300)
        >>> staff_member.name
        'staff'
        >>> staff_member.attack
        400
        >>> staff_member.defense
        300
        >>> other_staff = Card('other', 300, 500)
        >>> other_staff.attack
        300
        >>> other_staff.defense
        500
        """
        "*** YOUR CODE HERE ***"

    def power(self, other_card):
        """
        Calculate power as:
        (player card's attack) - (opponent card's defense)/2
        where other_card is the opponent's card.
        >>> staff_member = Card('staff', 400, 300)
        >>> other_staff = Card('other', 300, 500)
        >>> staff_member.power(other_staff)
        150.0
        >>> other_staff.power(staff_member)
        150.0
        >>> third_card = Card('third', 200, 400)
        >>> staff_member.power(third_card)
        200.0
        >>> third_card.power(staff_member)
        50.0
        """
        "*** YOUR CODE HERE ***"
```







### Q5: Making a Player

Now that we have cards, we can make a deck, but we still need players to actually use them. We'll now fill in the implementation of the class. `Player`

A instance has three instance attributes:`Player`

- `name` is the player's name. When you play the game, you can enter your name, which will be converted into a string to be passed to the constructor.
- `deck` is an instance of the class. You can draw from it using its method.`Deck``.draw()`
- `hand` is a list of instances. Each player should start with 5 cards in their hand, drawn from their . Each card in the hand can be selected by its index in the list during the game. When a player draws a new card from the deck, it is added to the end of this list.`Card``deck`

Complete the implementation of the constructor for so that is set to a list of 5 cards drawn from the player's .`Player``self.hand``deck`

Next, implement the and methods in the class. The method draws a card from the deck and adds it to the player's hand. The method removes and returns a card from the player's hand at the given index.`draw``play``Player``draw``play`

#### code

```
class Player:
    def __init__(self, deck, name):
        """Initialize a Player object.
        A Player starts the game by drawing 5 cards from their deck. Each turn,
        a Player draws another card from the deck and chooses one to play.
        >>> test_card = Card('test', 100, 100)
        >>> test_deck = Deck([test_card.copy() for _ in range(6)])
        >>> test_player = Player(test_deck, 'tester')
        >>> len(test_deck.cards)
        1
        >>> len(test_player.hand)
        5
        """
        self.deck = deck
        self.name = name
        "*** YOUR CODE HERE ***"

    def draw(self):
        """Draw a card from the player's deck and add it to their hand.
        >>> test_card = Card('test', 100, 100)
        >>> test_deck = Deck([test_card.copy() for _ in range(6)])
        >>> test_player = Player(test_deck, 'tester')
        >>> test_player.draw()
        >>> len(test_deck.cards)
        0
        >>> len(test_player.hand)
        6
        """
        assert not self.deck.is_empty(), 'Deck is empty!'
        "*** YOUR CODE HERE ***"

    def play(self, card_index):
        """Remove and return a card from the player's hand at the given index.
        >>> from cards import *
        >>> test_player = Player(standard_deck, 'tester')
        >>> ta1, ta2 = TACard("ta_1", 300, 400), TACard("ta_2", 500, 600)
        >>> tutor1, tutor2 = TutorCard("t1", 200, 500), TutorCard("t2", 600, 400)
        >>> test_player.hand = [ta1, ta2, tutor1, tutor2]
        >>> test_player.play(0) is ta1
        True
        >>> test_player.play(2) is tutor2
        True
        >>> len(test_player.hand)
        2
        """
        "*** YOUR CODE HERE ***"
```













# Pojects::ant:ant

**知识点：**

```
 def __str__(self):
        """返回一个对象的描述信息"""
        # print(num)
        return "名字是:%s , 年龄是:%d" % (self.name, self.age)
```

1. **在python中方法名如果是`__xxxx__()`的，那么就有特殊的功能，因此叫做“魔法”方法**
2. **当使用print输出对象的时候，只要自己定义了`__str__(self)`方法，那么就会打印从在这个方法中return的数据**
3. **`__str__`方法需要返回一个字符串，当做这个对象的描写**



------



```
repr(object)
>>> s = 'RUNOOB'
>>> repr(s)
"'RUNOOB'"
>>> dict = {'runoob': 'runoob.com', 'google': 'google.com'};
>>> repr(dict)
"{'google': 'google.com', 'runoob': 'runoob.com'}"


def __repr__(self):
     cname = type(self).__name__
     return '{0}({1}, {2})'.format(cname, self.armor, self.place)
```

调用repr时返回字符串形式的返回值





------

首先需要了解 __name__ 是属于 python 中的内置类属性，就是它会天生就存在于一个 python 程序中，代表对应程序名称。

比如所示的一段代码里面（这个脚本命名为 pcRequests.py），我只设了一个函数，但是并没有地方运行它，所以当 run 了这一段代码之后我们有会发现这个函数并没有被调用。但是当我们在运行这个代码时这个代码的 __name__ 的值为 __main__ （一段程序作为主线运行程序时其内置名称就是 __main__）。

```
import requests
class requests(object):
    def __init__(self,url):
        self.url=url
        self.result=self.getHTMLText(self.url)
    def getHTMLText(url):
        try:
            r=requests.get(url,timeout=30)
            r.raise_for_status()
            r.encoding=r.apparent_encoding
            return r.text
        except:
            return "This is a error."
print(__name__)
```

如果调用者是一个对象，那么就会返回这个对象的名字



------

```
dict.setdefault(key, default=None)
tinydict = {'runoob': '菜鸟教程', 'google': 'Google 搜索'}
print "Value : %s" %  tinydict.setdefault('runoob', None)
print "Value : %s" %  tinydict.setdefault('Taobao', '淘宝')
以上实例输出结果为：
Value : 菜鸟教程
Value : 淘宝
```

实际上是在对象中搜寻key值是否存在，若存在，则返回key值对应的value；否则，在对象中添加该key，并将key对应的值设置为default。





------

```
list.extend(seq)
aList = [123, 'xyz', 'zara', 'abc', 123];
bList = [2009, 'manni'];
aList.extend(bList)
print "Extended List : ", aList ;
输出
Extended List :  [123, 'xyz', 'zara', 'abc', 123, 2009, 'manni']
```

实际上是将extend里面的列表（单个数据）添加到调用extend的列表的末尾







------

！！！！！！！！！！若是子类可以通过调整父类而只需要修改属性而不必重构方法，那么就调整父类，子类的函数能尽量不重新书写就不重新书写





------

```
hasattr(object, name)                      如果对象有该属性返回 True，否则返回 False。
class Coordinate:
    x = 10
    y = -5
    z = 0
 
point1 = Coordinate() 
print(hasattr(point1, 'x'))               True
print(hasattr(point1, 'y'))               True
print(hasattr(point1, 'z'))               True
print(hasattr(point1, 'no'))              False
```









# Question

## Q5

```
  self.armor-=amount
        for i in self.place.bees[:]:
            i.reduce_armor(amount)
        if self.armor<=0:
            for i in self.place.bees[:]:
                i.reduce_armor(self.damage)
        Ant.reduce_armor(self,0)
```

其中的list[]与list[:]有啥区别，另外子类调用父类的函数，记得使用父类的类名调用









```
	 class QueenAnt(ThrowerAnt):  # You should change this line
# END Problem EC
    """The Queen of the colony. The game is over if a bee enters her place."""
    name = 'Queen'
    food_cost = 7
    flag=True
    is_watersafe = True
    # OVERRIDE CLASS ATTRIBUTES HERE
    # BEGIN Problem EC
    implemented = True   # Change to True to view in the GUI
    # END Problem EC

    def __init__(self, armor=1):
        # BEGIN Problem EC
        "*** YOUR CODE HERE ***"
        ScubaThrower.__init__(self,armor)
        self.flag=QueenAnt.flag
        QueenAnt.flag=False
        # END Problem EC

    def action(self, gamestate):
        """A queen ant throws a leaf, but also doubles the damage of ants
        in her tunnel.

        Impostor queens do only one thing: reduce their own armor to 0.
        """
        # BEGIN Problem EC
        "*** YOUR CODE HERE ***"
        if not self.flag:
            self.reduce_armor(self.armor)
        else:
            ScubaThrower.action(self,gamestate)
            self.double_damage_behind()
    def double_damage_behind(self):
        for ant in self.ants_behind():
            if ant and not ant.buffed and ant.damage:
                ant.damage=ant.damage*2
                ant.buffed=True
    def ants_behind(self):
        ants=[]
        p=self.place.exit
        while p is not None:
          ants.append(p.ant)
          p=p.exit
        return ants
    def remove_from(self, place):
        if not self.flag:
            Insect.remove_from(self,place)
        else:
            pass
```

