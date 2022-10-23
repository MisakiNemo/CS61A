# 进制

**十进制**

**八进制**

**二进制**

# Binary Number

计算方法

max value：pow(2,n)-1

## 为什么计算机使用二进制

**电流跟水流一样都是有波动的。如果是十进制等高进制，那么状态也就越多。那么当电流强一点或弱一点，就有可能会致使物理状态的改变，要么是让计算机的分辨能力更高（更多的花费 ，而且得不偿失），要么是使得计算更容易出现错误。但是如果是二进制，那么计算时就只有两种状态，0和1，即通电和不通电的情况。这样判断的时候即使电流有波动导致可能会有所差别，但很少会出现状态无法区分的情况。**

![image-20221010151640654](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010151640654.png)





# Signed Binary  Number

用符号表示符号（sign）：首位二进制数表示符号：0表示+（positive），1表示-（negative），这种表示方法易于人类理解，但是在计算机看来是相当笨拙的。而且若是当两个相反数相加时，和不会是0.因此这个不是一个好的计算方法



因此正常的方法是：一般将正常的二进制数看成是正数

![image-20221010152930266](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010152930266.png)

1为原码，2为补码，3为反码

![image-20221010153423378](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010153423378.png)

表示0的负数的时候，反码全为1，然后补码后向第四位进0，但是由于溢出（overflow），因此第四位不表示，所有000的负数仍是000





# Boolan Logic

与或非门

<img src="C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221011222419177.png" alt="image-20221011222419177" style="zoom:50%;" />





## Build Gate(transistors(晶体管))

<img src="C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221011223940192.png" alt="image-20221011223940192" style="zoom:50%;" />

可以看成电流从这个晶体管流过，若是input不接通，那么也就不会有输出，即输出为0.

### logic and gate

<img src="C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221011224529858.png" alt="image-20221011224529858" style="zoom:33%;" />

### logic or gate

<img src="C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221011224704809.png" alt="image-20221011224704809" style="zoom:33%;" />

### logic not gate

<img src="C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221011224914214.png" alt="image-20221011224914214" style="zoom:33%;" />

右边是输出，有一个电阻器