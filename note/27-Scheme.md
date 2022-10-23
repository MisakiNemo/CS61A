# Scheme

 

# Scheme Fundamentals

![image-20221019091220906](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221019091220906.png)

![image-20221019091551622](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221019091551622.png)



我的理解是，scheme的运算格式相当于前缀表达式，但是与前缀表达式不同的是，前缀表达式一个符号只对应两个运算的数， scheme会将括号中的所有运算数都按照前缀的运算符来计算。







# Special Forms

![image-20221019093343541](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221019093343541.png)

![image-20221019093925349](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221019093925349.png)

![image-20221019093949837](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221019093949837.png)





# 巴比伦算法求平方根

1. 猜测一个大于0近似值
2. 使用被开方数除以近似值
3. 计算前两步的数的平均值
4. 令该平均值为新的近似值，回到步骤2，循环计算

```
def square_root(n):
    root = n / 2
    for k in range(20):
        root = (1 / 2) * (root + (n / root))
    return root
print(square_root(6))
```





# Scheme Interpreters

学习scheme这门新语言的目的式为了了解计算机语言解释器是如何运行的





# Lambda Expressions

![image-20221019100546930](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221019100546930.png)





# Example:Sierpinski's Triangle(谢尔宾斯基三角形)

![image-20221019102014598](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221019102014598.png)

![image-20221019102134650](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221019102134650.png)





# More Speciial Forms

## Cond & Begin

![image-20221019102626970](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221019102626970.png)

cond:有多个条件判断的if...else...

begin:可以理解为开始一个代码块的标识符





## Let Expressions

![image-20221019103437504](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221019103437504.png)

let实际上是将变量赋值然后使用到之后的程序，可以在定义函数前使用		





# List

![image-20221019104924019](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221019104924019.png)





# Symbolic Programming

![image-20221019105540670](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221019105540670.png)

单引号是将后面的一个参数看成符号而不去先判断（评估/计算）它，如果没有单引号，那么计算机会首先去评估这个参数，并取值，然后用得到的值去创建一个新的变量或者进行操作



# Programs as Data

## A Scheme Expression is a Scheme List

![image-20221019110909103](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221019110909103.png)

![image-20221019111108204](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221019111108204.png)





# Generating Code(看不懂。。。)