# Box-and-Pointer Notation

Box:实际上是一个容器，能容纳各种数据的集合体

![image-20221010085207216](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010085207216.png)







# Slicing 

![image-20221010085620745](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010085620745.png)

```
list[start:end:step]    ，这种叫切片运算符，可以使用切片运算符生成一个新的list（或其他容器）
```







# Processing Container Values

![image-20221010090835225](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010090835225.png)





# Tree Abstraction

![image-20221010092841807](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010092841807.png)

![image-20221010092859245](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010092859245.png)







# Tree Process

参数中有树，返回值中也有树

#### 斐波那契数列树

![image-20221010142903620](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010142903620.png)









# Example :Print Tree







# Example:Suming Path

![image-20221010145352148](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010145352148.png)







# Lab05（后续先留着）- -干不动了

## Q1

![image-20221010170147783](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010170147783.png)

### code

```
 assert len(s) == len(t)
    "*** YOUR CODE HERE ***"
    return list([list(k) for k in  zip(s,t)])
```

知识点：py3种zip函数返回的是一个地址，因此需要使用循环遍历或者使用list将其转换，但是若是单独使用

```
若是这样：list(zip(s,t)),那么返回的就是[(1,2),(3,4)....]里面的是pair元素，
```





## Q2

![image-20221010173044518](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010173044518.png)

### code

```
    ct=make_city("ex",lat,lon)
    dis1=distance(ct,city_a)
    dis2=distance(ct,city_b)
    return get_name(city_a) if dis1<=dis2 else get_name(city_b)
```

但是原本写了一个只有一行的解法	

## Q3

![image-20221010173023281](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010173023281.png)

### code

```
 ct=make_city("ex",lat,lon)
    dis1=distance(ct,city_a)
    dis2=distance(ct,city_b)
    return get_name(city_a) if dis1<=dis2 else get_name(city_b)
```







## Q5

![image-20221010184737791](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010184737791.png)

### code

```
    if label(t)=="berry":
        return True
    else:
        for branch in branches(t):
            if  berry_finder(branch):
                return True
        return False
```





## Q6

![image-20221010192935378](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010192935378.png)

### code(别人的)

```
 if is_leaf(t):
        return tree(label(t), [tree(x) for x in leaves])
    else:
        return tree(label(t), [sprout_leaves(branch, leaves) for branch in branches(t)])
```





## Q8

![image-20221011184017365](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221011184017365.png)

### code

```
return list([x,fn(x)] for x in seq if fn(x)>=lower and fn(x)<=upper)
```





## Q9

![image-20221010201455592](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221010201455592.png)

### code(other)

```
  M=len(deck)//2
    return    [deck[k//2+M*(k%2)] for k in range(len(deck))]
```







## Q10（不会）

![image-20221011184643124](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221011184643124.png)

### code

```
 if is_leaf(t1):
        return tree(label(t1) + label(t2), branches(t2))
    elif is_leaf(t2):
        return tree(label(t1) + label(t2), branches(t1))
    else:
        fewer_branch_t, more_branch_t = sorted([branches(t1), branches(t2)], key=len)
        pad_t1 = fewer_branch_t + [tree(0) for i in range(len(more_branch_t) - len(fewer_branch_t))]
        pad_t2 = more_branch_t
        return tree(label(t1) + label(t2),\
                [add_trees(b1, b2) for b1, b2 in zip(pad_t1, pad_t2)])
```

