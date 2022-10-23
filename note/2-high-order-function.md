## High-order-function(高阶函数)

**指参数中或者返回值有其他函数的函数就是高阶函数**，**可以直接调用传入的函数**，**将函数作为参数传入另一个函数或者将函数作为返回值返回**



函数作为参数返回

![image-20221003173201662](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221003173201662.png)

## lambda（匿名函数）

匿名函数

![image-20221003174111040](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221003174111040.png)

## 反函数

求反函数的代码：但是这个逻辑搞不太懂，**看一下Q&A**

<img src="C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221003190004455.png" alt="image-20221003190004455" style="zoom:50%;" />

**y为f（x）的一个值，lambda返回一个函数，传入y值，返回f（x）中x值的函数**

## control

**为什么需要有if...else语句**

![image-20221003193929487](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221003193929487.png)

如果像里面使用real_sqrt函数来作判断来使用更优方案会导致错误，因为函数会在运行前会评估（计算）所有的组成部分。也就是当传入为-4时，里面的if_会判断sqrt（x）是否合理。这时候sqrt（-4）就因为不符合规则而报错，整个部分也就无法运行。

但是当使用if...else：不会需要先运行条件判断对错之后的所有语句。而是在先判断条件是否成立的情况下运行相对应的语句，这时候就不会产生任何错误。

## control—expression

![image-20221003195140354](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221003195140354.png)

通过短路效果，如果判断语句后面有崩溃的特殊点，那么可以使用短路效果，将特殊点放在前面使用and 和or将这个特殊点给短路了，这样，即使运行时遇到特殊点，那么也不会导致崩溃

# log





assert函数：格式为     assert   condition,"error output statement"![image-20221003212638607](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221003212638607.png)

**assert 的作用是现计算表达式 expression ，如果其值为假（即为0），那么它先向 stderr 打印一条出错信息,然后通过调用 abort 来终止程序运行。**









![image-20221003212937426](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221003212937426.png)

randint(n,m):返回n-m之间的随机整数值



nonlocal函数:

[^]: 非局部声明变量指代的已有标识符是最近外面函数的已声明变量，但是不包括全局变量。这个是很重要的，因为绑定的默认行为是首先搜索本地命名空间。nonlocal声明的变量只对局部起作用，离开封装函数，那么该变量就无效。非局部声明不像全局声明，我们必须在封装函数前面事先声明该变量非局部声明不能与局部范围的声明冲突

![image-20221003213506663](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221003213506663.png)

通俗来说，nonlocal函数是在局部环境中的定义一个新的函数或创建的一个新的环境中使用局部环境的变量声明时需要使用。但是如果该定义变量是在全局变量中定义的，即该变量不在局部变量中，那么不可使用。**这里面使用是为了保存index的值，以达成多次调用时返回的是不断递增的值。**

 





![image-20221003214306343](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221003214306343.png)

另外，这里该函数传入的是一个指针，可以代表一个地址，数组...因此在后面例子中的1，2，3就被当成是一个数组，在该函数中使用outcome[n]便可按顺序调用这些值。





### problem-6

![image-20221005084924248](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221005084924248.png)

看不太懂，这里的echo，total返回那里，**不过这里得说一句，这种高阶函数交替使用两个多个（两个）函数的方式很妙**





**这里这个直接返回，但是赋值之后，会因为先判断两个参数，所以f(score0,score1)和g(score0,score1)会先直接被运行，然后才是返回一个相同的函数，这样就可以无限套娃使用下去了。**

如果是正常的话，就是在循环里面正常分别调用两个函数，或者使用一样的语句，这里是直接在循环里面赋值就行了。

**tql，这种循环使用使用函数的思路**。

另外，如果是这样使用的话，有一个限制条件：就是参数调用的两个函数g和f的返回值必须为一个函数：

如果返回值为本身的话，就意味着为自身的不断调用

如果返回值为对方（其他几个）函数，且函数构成闭环，那么就是循环不断调用这几个函数

![image-20221005092228652](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221005092228652.png)



### program-7

**我真的看不懂啊啊啊啊啊啊啊啊，高阶函数里创建一个子函数，然后子函数返回父函数，然后父函数返回子函数？？？？？？？？？？？？？？？？？？？？？？？？？？？？**

![image-20221005100247188](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221005100247188.png)

**看懂了。。。这玩意自己怎么可能写得出来啊。。。就真的太离谱了。高阶函数得玩法真的花。。。**

**太离谱了！！！！太离谱了！！！太离谱了！！！**

**当返回值不带括号时以及参数时，那么就是代表着返回这个函数本身。当有括号和返回值时，那么就代表着返回的是这个函数的返回值！！！**







![image-20221005112051837](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221005112051837.png)



多重循环里面的循环变量不能相同

![image-20221005132448429](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221005132448429.png)



## highest-order-function usage

**必须得清晰知道每一个和函数的作用**，**这是能写出好代码的关键**。**这个函数是否是高阶函数，是要做什么的，一个一个螺丝去制作，才能把整个项目给做好**

