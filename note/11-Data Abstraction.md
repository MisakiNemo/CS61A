

# Data Abstraction

![image-20221008100557001](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221008100557001.png)





# Pair

![image-20221008101626800](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221008101626800.png)

```
gcd:返回两个数的最大公约数
```





## Abstraction Barrier







# Data representation

## pre

![image-20221008103518628](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221008103518628.png)



## aft

![image-20221008103434343](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221008103434343.png)

**差别：pre中的选取分子和分母都是通过numer和denom本身去选取的，但是aft中选取分子和分母，并不是通过numer和demom直接选取，而且通过调用x返回的select函数去选取**   这种差别就将











# Disc

## Q1

![image-20221008104809528](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221008104809528.png)

### Answer

#### Code

```
def count_stars_way(n):
    if n==0 or n==1:
        return 1
    elif n<0:
        return 0
    else:
        return count_stars_way(n-1)+count_stars_way(n-2)
print(count_stars_way(2))
```

**A2:最简单的输出是当只剩1个或者0个台阶时，返回一个（一种方法），当台阶数小于0时，则说明没有方法**

**A3：count(n-1)代表当前走一步之后走剩下的台阶的方法个数，count(n-2)代表当前走两步之后走剩下台阶的方法个数**

### Plus（不会）

**个人对这道问题的理解是：c_p算法的延伸，与c_p算法不同的是，这道题有次序之分(c_p算法在recursion tree中)**

![image-20221008105854343](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221008105854343.png)

#### code

```
def count_k(n,k):
```



## Q2







# Cats

## Q1

![image-20221008223019387](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221008223019387.png)

### code

```
 count=0
    for s in paragraphs:
        if select(s) and count==k:
            return s
        elif select(s):
            count+=1
    return ''
```



## Q2



![image-20221008223125487](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221008223125487.png)

### code

```
    def helper(s):
        for k in topic:
            for n in remove_punctuation(lower(s)).split():
                if lower(k)==n:
                    return True
        return False
    return helper
```

#### 知识点：

**函数 remove_punctuation:移除字符串里面的所有标点符号**

**如果不区分大小写匹配，那么可以使用lower或upper将两个要对比的字符串全都转换成大写或者小写**

**补充：函数title可以将每个单词的首个字母大写**

```
str = "www.runoob.com"                                          
print(str.upper())          WWW.RUNOOB.COM                   # 把所有字符中的小写字母转换成大写字母     
print(str.lower())          www.runoob.com                   # 把所有字符中的大写字母转换成小写字母
print(str.capitalize())      Www.Runoob.Com                  # 把第一个字母转化为大写字母，其余小写
print(str.title())          Www.Runoob.Com                   # 把每个单词的第一个字母转化为大写，其余小写 
```





## Q5

![image-20221009100043574](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221009100043574.png)

![image-20221009094821311](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221009094821311.png)

### code

```
 if user_word in valid_words:
        return user_word
    word_diff=[diff_function(user_word,s,limit) for s in valid_words]
    word,dif=min(zip(valid_words,word_diff),key=lambda item:item[1])
    if dif >limit:
        return user_word
    else:
        return word
```

**知识点**

**min函数和zip函数的用法**



## Q6

![image-20221009102525234](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221009102525234.png)

使用递归求解

#### **知识点**

```
strname[index]
url = 'http://c.biancheng.net/python/'
print(url[10])          结果为i                               #获取索引为10的字符（从0开始）
print(url[-6])          结果为y                               #获取倒数索引为 6 的字符（从1开始）

```

```
strname[start : end : step]
url = 'http://c.biancheng.net/java/'
#获取索引从7处到22（不包含22）的子串
print(url[7: 22]) # 输出 c.biancheng.net
#获取索引从7处到-6的子串
print(url[7: -6]) # 输出 c.biancheng.net
#获取索引从-21到6的子串
print(url[-21: -6]) 输出  c.biancheng.net
#从索引3开始，每隔4个字符取出一个字符，直到索引22为止
print(url[3: 22: 4])         pcaen
```

#### code

```
我的：
def helper(s,g,count):
    
       if len(s)==0 or len(g)==0 or count>limit:
           return abs(len(s)-len(g))+count
       else:
           return helper(s[1:],g[1:],count+1 if s[0]!=g[0] else count)
    return helper(start,goal,0)
    
    
别人的：
if len(start) == 0:
        return len(goal)
    if len(goal) == 0:
        return len(start)
    if start[0] != goal[0]:
        if limit == 0:
            return 1
        return 1 + shifty_shifts(start[1:], goal[1:], limit - 1)
    else:
        return shifty_shifts(start[1:], goal[1:], limit)
```

**思路大差不差，原本我也打算直接递归给出的函数而不是用高阶函数**







## Q7

![image-20221009190628204](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221009190628204.png)

#### code(别人的，自己的死活运行错误)

```
 if limit < 0:
        # BEGIN
        "*** YOUR CODE HERE ***"
        return 0
        # END

    elif len(start) == 0 or len(goal) == 0:
        # BEGIN
        "*** YOUR CODE HERE ***"
        return len(start) + len(goal)
        # END
    elif start[0] == goal[0]:
        return pawssible_patches(start[1:], goal[1:], limit)
    else:
        add_diff = pawssible_patches(start, goal[1:], limit - 1)
        remove_diff = pawssible_patches(start[1:], goal, limit - 1)
        substitute_diff = pawssible_patches(start[1:], goal[1:], limit - 1)
        # BEGIN
        "*** YOUR CODE HERE ***"
        return 1 + min(min(add_diff, remove_diff), substitute_diff)
        # END
```

**一定要清楚知道递归函数的作用是什么！！！！！把递归函数在自身能用本身替代的部分都替代掉**

**自己的**(无法运行)

```
 if len(start)==0: # Fill in the condition
        # BEGIN
        "*** YOUR CODE HERE ***"
        return len(goal)
        # END

    elif len(goal): # Feel free to remove or add additional cases
        # BEGIN
        "*** YOUR CODE HERE ***"
        return  len(start)
        # END
    elif start[0]==goal[0]:
            return pawssible_patches(start[1:],goal[1:],limit)
    else:
            if limit==0:
                return 1
            add_diff =goal[0]+start # Fill in these lines
            remove_diff =start[1:]
            substitute_diff =goal[0]+start[1:]
        # BEGIN
        "*** YOUR CODE HERE ***"
            str=[add_diff,remove_diff,substitute_diff]
            shift_num=[shifty_shifts(start=s,goal=goal,limit=limit) for s in str]
            new,minu=min(zip(str,shift_num),key=lambda item:item[1])
            return pawssible_patches(new,goal,limit-1)+1
```





## Q8

![image-20221009194617543](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221009194617543.png)

#### code

```
    count=0
    for i in range(min(len(typed),len(prompt))):
         if typed[i]==prompt[i]:
              count=count+1
         else:
             break
    progress=count/len(prompt)
    report={
        'id':user_id,
        'progress':progress
    }
    send(report)
    return progress
```

##### **知识点：**

创建结构体的语法





## Q9

![image-20221009202813371](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221009202813371.png)

```
    ts=[]
    for player_time in times_per_player:
        per_time=[player_time[i]-player_time[i-1] for i in range(1,len(player_time))]
        ts+=[per_time]
    return game(words,ts)
```





## Q10

![image-20221009214342487](C:\Users\vigor\AppData\Roaming\Typora\typora-user-images\image-20221009214342487.png)

#### code

```
 player_indices = range(len(all_times(game)))  # contains an *index* for each player
    word_indices = range(len(all_words(game)))    # contains an *index* for each word
    # BEGIN PROBLEM 10
    "*** YOUR CODE HERE ***"
    fastest=[[] for _ in range(len(all_times(game)))]
    for i ,word in enumerate(all_words(game)):
        word_time=[all_times(game)[player][i] for player in player_indices]
        player_index=min(player_indices,key=lambda x:word_time[x])
        fastest[player_index].append(word)
    return fastest
```

#### **知识点**

#####  enumerate() 函数

```
enumerate(sequence, [start=0])   传入一个list列表


>>> seasons = ['Spring', 'Summer', 'Fall', 'Winter']
>>> list(enumerate(seasons))
[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
>>> list(enumerate(seasons, start=1))       # 下标从 1 开始
[(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
```

