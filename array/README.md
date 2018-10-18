# Array
Python achieve many array

容器序列：
list、 tuple、 collections.deque 这些序列可以存放不同类型的数据

扁平序列：
str、bytes、bytearray、memoryview和array.array 这些序列可以存放一种类型的数据

序列可以分为可变序列与不可变序列：


可变序列：
str、bytearray、memoryview和array.array、list、collections.deque 


不可变序列:
tuple、str和bytes


不可变序列内置:__iter__,__contains__,__len__,__getitem__,__reversed__,index,count


可变序列内置:__setitem__,__delitem__,insert,append,reverse,extend,pop,remove,__iadd__,以及(继承了不可变)


对于list来说，在python2.X中，for处理可能会影响上下文的同名变量
* a = 'abc'
* dummy = [a for a in 'abc']
* a
* 'c'

但是在python3中，采用了局部作用域。表达式内部的变量和赋值只在局部起作用，表达式的上下文同名变量还可以正常被引用，对于列表推导与fiter结合map可以做的事情，它都可以做，而且还不需要lambda表达式
* symbols = '$¢£¥€¤'
* beyond_ascii = [ord(s) for s in symbols if ord(s) > 127]
* beyond_ascii = list(filter(lambda c: c > 127, map(ord, symbols)))


对于列表推导来说，它就是生成一个列表，对于其他的类型的序列，生成器表达式可以实现

# tuple　
* 元组拆包，占位符_，*匹配忽略多余的元素
* python中我们常用*args匹配不确定数量的参数,python3中也被用于赋值
* a, b, *rest = range(5) 
* a, b, rest
* (0, 1, [2, 3, 4])


* 具名元组：collections.nametuple 继承了元组
* nametuple传递两个参数:类名，还有一个可迭代对象,或者空格分开的字段名组成的字符串
* _fields类属性，获取其所有类字段，_make接受可迭代对象生成这个类的一个实例，_asdict把具名元组以collection.orderdict形式返回

# 切片
* python中list,tuple,str这类序列都支持切片操作，注意在列表切片的时候，切片的对象是个序列
* l1 = [1, 2, 3, 4, 5]
* l1[2:3] = 100 这是错误的 
* l1[2:3] = [100]　需要将赋值改成可迭代的对象

对于序列的增量来说，+=,*=运算方式都是一样，+=实现的方发为__iadd__,倘若没有实现这个方法就使用__add__方法，
* a += b，在这个表达式中，变量名会不会被关联到新的对象，完全取决于实现了__iadd__方法
* 当然对于*=来说也就是实现了__imul__,


对于可变序列与不可变序列，增量是两种：
* l = [1, 2, 3]
* id(l) #140470157591304
* l *= 2 
* id(l) #140470157591304

* l = (1, 2, 3)
* id(l) #140470157610152
* l *= 2 
* id(l) #140470188072296
* 对于元组，它取了新的一个地址，然后再赋值，说明对于不可变的序列进行重复操作，它每次都会生成一个新的对象
 
python tutor 内存可视化，dis.dis()操作显示字节码 增量并不是原子操作，虽然会完成操作，但是会报异常，tuple object does not support item assignment
