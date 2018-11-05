# My_Python
summed up my experience about python


python 一切皆对象 这句话的根据：在python中，type,object,class之间的关系便阐明了这句话。比如: list, str, dict, tuple的基类就是type,　然而都继承于object,在python2中一般都是写成class A(object):pass  然在python3中写成class B:pass 对于object来说它又是type的实例，type继承于object，而type的实例是它自己，所以一切皆对象，object是多有类的基类，一切都基于object。

关于编码unicod, utf-8编码问题，在我们从文件读取的时候将utf-8编码转化为unicode编码（编码问题），统一处理，存入文件（空间的问题）的时候转化为utf-8，python2中有两种编码格式string,unicode, window下，比如s="我" 默认gb2312编码 s.decode("gb2312").encode("utf8"),s=u"我" s.encode("utf8")
对于python3中字符内置成unicode类型

