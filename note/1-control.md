

## print and none:

![image-20221003092651699](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221003092651699.png)
 python 解释器不会将None输出，但是print会。另外print是一个操作函数，无返回值(也就是None)但是会将输入的数据打印出去
 这就是为什么会出现以上的结果了

## Multiple Environment

**环境是一系列框架的总称**

在py中，使用def定义一个函数后，后面的语句缩进代表该语句在该框架中运行，如果没有缩进，则代表该语句是与def语句为同一层次的，在同一个父环境中。

 **当调用一次函数时新创建一个框架，在这个框架中的变量是独立存在的，**不与其他的函数环境或者global环境相冲突。

因此当递归调用一个函数时，会在每次递归时都创建一个新的框架（flame），即使递归中使用的变量名都是一样的，也不会发生冲突。



<img src="C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221003094255482.png" alt="image-20221003094255482" style="zoom:50%;" />

## 条件语句：

## 循环语句：