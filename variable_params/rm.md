      在传递函数参数的时候,　不要使用可变类型作为函数的参数默认值
      # def foo(arg1, l1=[]):
      #     l1.append(arg1)
      #     print(l1)
      #
      # foo(2)
      # foo(1, l1=[3, 4])
      # foo(5)

      class Foo:

          def __init__(self, l1=[]):
              self.l1 = l1

          def add(self, arg1):
              self.l1.append(arg1)

          def delete(self, arg1):
              self.l1.remove(arg1)


      f = Foo()
      f.add(2)
      print(f.l1)
      f1 = Foo([1])
      f1.add(3)
      print(f1.l1)
      f2 = Foo()
      f2.add(4)
      print(f2.l1)
      print(Foo.__init__.__defaults__)
      print(f2.l1 is f.l1)
      #
      # def foo(arg1, l1=None):
      #     if l1 is None:
      #         l1 = []
      #     l1.append(arg1)
      #     print(l1)
      #
      #
      # foo(2)
      # foo(1, l1=[3, 4])
      # foo(5)

      # class Foo:
      #
      #     def __init__(self, l1=None):
      #         if l1 is None:
      #             self.l1 = []
      #         else:
      #             self.l1 = l1  #注意这一行self.l1变成了l1的别名
      #
      #     def add(self, arg1):
      #         self.l1.append(arg1)
      #
      #     def delete(self, arg1):
      #         self.l1.remove(arg1)



      #
      # class Foo:
      #
      #     def __init__(self, l1=None):
      #         if l1 is None:
      #             self.l1 = []
      #         else:
      #             # copy like next sample produce error
      #             self.l1 = list(l1)
      #
      #     def add(self, arg1):
      #         self.l1.append(arg1)
      #
      #     def delete(self, arg1):
      #         self.l1.remove(arg1)
      #
      #
      # l = [1, 2, 3, 4, 5]
      # f = Foo(l)
      # f.delete(1)
      # f.delete(2)
      # print(l)
      # print(Foo.__init__.__defaults__)
