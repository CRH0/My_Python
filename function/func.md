# 构造任意数量参数的函数

def avg (first, * rest):  
return (first + sum(rest)) / (1 + len(rest))

avg(1, 2) # 1.5

avg(1, 2, 3, 4) # 2.5
在这个例子中,rest是由所有其他位置参数组成的元组。然后我们在代码中把它当成了一个序列来进行后续的计算。

为了接受任意数量的关键字参数,使用一个以**开头的参数。























  
