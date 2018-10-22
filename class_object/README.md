    # 你想改变对象实例的打印或显示输出,让它们更具可读性
  
    class Pair: 
  
      def __init__(self, x, y):
          self.x = x
          self.y = y

      def __repr__(self):
          return 'Pair({0.x!r},{0.y!r})'.format(self)

      def __str__(self):
          return '({0.x!r},{0.y!r})'.format(self
     p = Pair(3, 4)
     print(p)


    
    # 你想通过format()函数和字符串方法使得一个对象能支持自定义的格式化。

    _formats = {
       'ymd': '{d.year}-{d.month}-{d.day}',
       'mdy': '{d.month}/{d.day}/{d.year}',
       'dmy': '{d.day}/{d.month}/{d.year}'
     }


    class Date:
        def __init__(self, year, month, day):
            self.day = day
            self.month = month
            self.year = year
    def __format__(self, code):
        if code == '':
            code = 'ymd'
        fmt = _formats[code]
        return fmt.format(d=self)


     d = Date(2018, 10, 21)
     print(format(d, 'dmy'))



    # 你想封装类的实例上面的“私有”数据,但是Python语言并没有访问控制。
    # 解决方案
    # Python程序员不去依赖语言特性去封装数据,而是通过遵循一定的属性和方法命名规约
    # 来达到这个效果。 第一个约定是任何以单下划线_开头的名字都应该是内部实现。

    # class A:
    #     def __init__(self):
    #         self._internal = 0  # An internal attribute
    #         self.public = 1  # A public attribute
    #
    #     def public_method(self):
    #         '''
    #         A public method
    #         '''
    #         pass
    #
    #     def _internal_method(self):
    #         pass
    #

    # a = A()
    # print(a.public)
    # print(a._internal)



    # Python并不会真的阻止别人访问内部名称。但是如果你这么做肯定是不好的,可能会导
    # 致脆弱的代码。 同时还要注意到,使用下划线开头的约定同样适用于模块名和模块级别
    # 函数。 例如,如果你看到某个模块名以单下划线开头(比如_socket),那它就是内部实现。
    # 类似的,模块级别函数比如 sys._getframe() 在使用的时候就得加倍小心了。

    # 你还可能会遇到在类定义中使用两个下划线(__)开头的命名
    # class B:
    #     def __init__(self):
    #         self.__private = 0
    #
    #     def __private_method(self):
    #         pass
    #
    #     def public_method(self):
    #         pass
    #         self.__private_method()


    # b = B()
    # print(b._B__private)
    # class C(B):
    #     def __init__(self):
    #         super().__init__()
    #         self.__private = 1  # Does not override B.__private
    #
    #     # Does not override B.__private_method()
    #     def __private_method(self):
    #         pass

    #
    # class Base:
    #     def __init__(self):
    #         print('Base.__init__')
    #
    #
    # class A(Base):
    #     def __init__(self):
    #         Base.__init__(self)
    #         print('A.__init__')
    #
    #
    # class B(Base):
    #
    #     def __init__(self):
    #         Base.__init__(self)
    #         print('B.__init__')
    #
    #
    # class C(A, B):
    #
    #     def __init__(self):
    #         A.__init__(self)
    #         B.__init__(self)
    #         print('C.__init__')

    # c = C()


    class Base:
        def __init__(self):
            print('Base.__init__')


    class A(Base):
        def __init__(self):
            super().__init__()
            print('A.__init__')


    class B(Base):

        def __init__(self):
            super().__init__()
            print('B.__init__')


    class C(A, B):

        def __init__(self):
            super().__init__()
            # B.__init__(self)
            print('C.__init__')
            
    c = C()
