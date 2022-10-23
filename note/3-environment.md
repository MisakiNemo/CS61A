



# Environment for higher-order-function

![image-20221005154733853](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221005154733853.png)

**当前环境中如果没用使用的函数，会一层一层地往外找。当前环境中->父环境......->全局环境**





# Environment for nested definitions

![image-20221006082045301](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006082045301.png)

***当前环境中如果没用使用的函数，会一层一层地往外找。当前环境中->父环境......->全局环境**。

***当前环境中如果没用使用的函数，会一层一层地往外找。当前环境中->父环境......->全局环境***

，

#### draw an environment diagram 

![image-20221006083058845](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006083058845.png)





# local name

![image-20221006083836705](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006083836705.png)

每个函数调用时，都会创建一个独立的环境。当在一个当前环境中调用另一个函数（该函数并非在当前环境中创建，而是在全局环境中创建时），会在该环境之外再创建一个独立环境。当新创建的独立环境中使用到当前环境中变量时，在新创建的环境中找不到时，会返回它的父环境中寻找（全局环境）。此时就会报错。

**但是嵌套函数的话就不会发生这种情况。因为嵌套函数中的函数会一层一层地往父环境方向寻找**







## Function Composition

![image-20221006084922859](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006084922859.png)





# lambda

![image-20221006085728637](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006085728637.png)

### versus

![image-20221006085752861](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006085752861.png)

![image-20221006085832882](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006085832882.png)

![image-20221006090255784](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006090255784.png)

**即使将square赋值给另一个名称，但函数本身绑定的还是原来的名字square****







# Self-reference

![image-20221006090627348](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006090627348.png)

![image-20221006091856148](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006091856148.png)

太强了！！！



# currying

![image-20221006093033375](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221006093033375.png)

**将多参函数变成单参高阶函数的方法叫currying**