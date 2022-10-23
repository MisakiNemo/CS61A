# The structure of an Interpreter

![image-20221021124941451](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221021124941451.png)





# Special Forms

![image-20221021143513263](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221021143513263.png)





# Logical Forms

![image-20221021144119183](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221021144119183.png)





# Quotation

![image-20221021144901859](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221021144901859.png)

当遇到'和“quote”时，解释器会将其转换，并且在遇到‘之后不会再去运行（判断）后面的exp





# Lambda Expression







![image-20221021150031179](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221021150031179.png)



![image-20221021150052643](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221021150052643.png)

![image-20221021150018054](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221021150018054.png)

框架也是一种数据类型，实际上每个框架都是一个对象。既然是数据类型，那就可以被当成参数传入和传出。。。。。跟高阶函数一样。。。

所以以前学的都是有意义的，真的太啊美景了







# Define Expressions

![image-20221021151127482](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221021151127482.png)

当使用定义时，会将表达式中的参数（value）转换成一个匿名函数，在评估调用完该函数的时候并传回值的时候才会给定义的名称赋值，而赋值之后，如何获得该值的过程不会被记录



# Apply User-Defined  Procedures

![image-20221021152010843](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221021152010843.png)

、









# Lab11

```y
buffer
```

**一定要对传入传出的参数的数据类型清楚明了！！！**不然你都不知道如何使用传入的参数







# Project
