# String Representation

![image-20221018083158731](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018083158731.png)





## The Repr String for an Object

![image-20221018083513349](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018083513349.png)

返回的是计算机阅读的**可运行**的python语句，因此可以使用eval运行repr返回的结果

### Eval

```
eval(expression[, globals[, locals]])
expression -- 表达式。
globals -- 变量作用域，全局命名空间，如果被提供，则必须是一个字典对象。
locals -- 变量作用域，局部命名空间，如果被提供，可以是任何映射对象。
>>>x = 7
>>> eval( '3 * x' )
21
>>> eval('pow(2,2)')
4
>>> eval('2 + 2')
4
>>> n=81
>>> eval("n + 4")
85
```

```
eval(repr(object))=object
```



## The str String for an Object

![image-20221018084448826](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018084448826.png)

返回的是一个符合人类阅读习惯的str语句，不可执行，因此不可以使用eval运行





## Example

![image-20221018084735592](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018084735592.png)

![image-20221018084719093](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018084719093.png)





# Polymophic functions

![image-20221018085143569](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018085143569.png)

类中的内置方法和函数，无参，直接调用即可



## Implement repr and str

![image-20221018090321033](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018090321033.png)

如果是直接使用str()或者repr(),即使该对象存在自己独立的同名函数和方法，那么也会返回类中的__repr__和__str__.若是通过dot调用，那么就会按照类和对象的调用方法从下往上调用





# Special Method Names in Python

![image-20221018092230787](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018092230787.png)

### add

![image-20221018092505374](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018092505374.png)

### gcd

![image-20221018092754322](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018092754322.png)



### example(important)

![image-20221018094325043](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221018094325043.png)

若是位置不同的话，就A+B与B+A相同，那么需要

```
__radd__=__add__
```

否则，重新定义radd(reversed add)

#### isinstance()

```
isinstance(object, classinfo)
object -- 实例对象。
classinfo -- 可以是直接或间接类名、基本类型或者由它们组成的元组。
>>>a = 2
>>> isinstance (a,int)
True
>>> isinstance (a,str)
False
>>> isinstance (a,(str,int,list))    # 是元组中的一个返回 True
True
```

