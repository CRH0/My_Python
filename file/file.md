      f = open('sample.txt', 'rt', encoding='ascii')


      f.read()
      # 读取文本的时候注意文件编码,如果编码错误的话,试着给open()函数传递一个errors参数
      f = open('sample.txt', 'rt', encoding='ascii', errors='replace')


      f.read()


      g = open('sample.txt', 'rt', encoding='ascii', errors='ignore')


      g.read()

      # 你想将print()函数的输出重定向到一个文件中去。
      # 在print()函数中指定file关键字参数,像下面这样:

      with open('d:/work/test.txt', 'wt') as f:


        print('Hello World!', file=f)
      # 讨论
      # 关于输出重定向到文件中就这些了.但是有一点要注意的就是文件必须是以文本模式打开.
      # 如果文件是二进制模式的话,打印就会出错.

      # 问题:
      # 你想使用print()函数输出数据,但是想改变默认的分隔符或者行尾符。

      # 解决方案
      # 可以使用在print()函数中使用sep和end关键字参数,以你想要的方式输出.
      print('ACME', 50, 91.5, sep=',')


      print('ACME', 50, 91.5, sep=',', end='!!\n')
      # 讨论
      # 当你想使用非空格分隔符来输出数据的时候,给print()函数传递一个seq参数是最简单的方案.
      # 有时候你会看到一些程序员会使用str.join()来完成同样的事情.
      ''.join(('A','B','C')) 正确


      ''.join(('A','B',3))　　错误

      # 如果你想从二进制模式的文件中读取或写入文本数据,必须确保要进行解码和编码操作
       with open('somefile.bin', 'rb') as f:


          data = f.read(16)


          text = data.decode('utf-8')


       with open('somefile.bin', 'wb') as f:


        text = 'Hello World' 

       f.write(text.encode('utf-8'))
      # 二进制I/O还有一个鲜为人知的特性就是数组和C结构体类型能直接被写入,而不需要中间转换为自己对象
      * import array
      * nums = array.array('i', [1, 2, 3, 4])
      * with open('data.bin', 'wb') as f:
      *     f.write(nums)

      # 写文件时通常会遇到的一个问题的完美解决方案(不小心覆盖一个已存在的文件)
      #  一个替代方案是先测试这个文件是否存在,像下面这样:
      * import os
      * 
      * if not os.path.exists('somefile'):
      *     with open('somefile', 'wt') as f:
      *         f.write('Hello\n')
      * else:
      *     print('File already exists!')
      # 你想像一个文件中写入数据,但是前提必须是这个文件在文件系统上不存在。 也就是不
      # 允许覆盖已存在的文件内容 可以在open() 函数中使用 x 模式来代替w 模式的方法来解决这个问题
      # x模式是python3对open()函数特有的拓展

      # 　字符串的I/O操作,接口操作
      * import io

      # 操作文本
      * s = io.StringIO()
      * s.write('Hello World\n')
      * print('This is a test', file=s)
      * s.getvalue()
      * s = io.StringIO('Hello\nWorld\n')
      * s.read(4)
      * s.read()

      # 操作二进制数据
      * s = io.BytesIO()
      * s.write(b'binary data')
      * s.getvalue()

      # 读取压缩文件
      * gzip compression
      * import gzip
      * 
      * with gzip.open('somefile.gz', 'rt') as f:
      *     text = f.read()
      * bz2 compression
      * import bz2
      #
      * with bz2.open('somefile.bz2', 'rt') as f:
      *     text = f.read()
      #
      * import gzip
      #
      * f = open('somefile.gz', 'rb')
      * with gzip.open(f, 'rt') as g:
      *     text = g.read()


      # 文件路径名的操作
      # 问题
      # 你需要使用路径名来获取文件名,目录名,绝对路径等等.
      # os.path模块中的函数来操作文件名
      * import os
      #
      * path = '/Users/beazley/Data/data.csv'
      *  Get the last component of the path
      * os.path.basename(path)
      * Join path components together
      * os.path.join('tmp', 'data', os.path.basename(path))
      * path = '~/Data/data.csv'
      * os.path.expanduser(path)
      * '/Users/beazley/Data/data.csv'
      * Split the file extension
      * os.path.splitext(path)
      * ('~/Data/data', '.csv')

      # 测试文件是否存在
      # 问题
      # 你想测试一个文件或目录是否存在。
      * import os
      * os.path.exists('/etc/passwd')
      * True
      * os.path.exists('/tmp/spam')
      * False
      * Is a regular file
      * os.path.isfile('/etc/passwd')
      * True
      * Is a directory
      * os.path.isdir('/etc/passwd')
      * False
      * Is a symbolic link
      * os.path.islink('/usr/local/bin/python3')
      * True  # Get the file linked to
      * os.path.realpath('/usr/local/bin/python3')
      * '/usr/local/bin/python3.3'
      # 获取文件夹中的文件列表
      # 问题
      # 你想获取文件系统中某个目录下的所有文件列表.
      * import os
      * names = os.listdir('somedir')
      # 获取目录文件夹下面所有文件
      * Get all regular files
      * names = [name for name in os.listdir('somedir')
      *          if os.path.isfile(os.path.join('somedir', name))]

      # 获取目录文件夹
      * Get all dirs
      * dirnames = [name for name in os.listdir('somedir')
      *             if os.path.isdir(os.path.join('somedir', name))]

      # 字符串的startswith()和endswith()方法对于过滤一个目录的内容也是很有用的.
      * pyfiles = [name for name in os.listdir('somedir')
      *            if name.endswith('.py')]


      # 对于文件名的匹配,你可能会考虑使用glob或fnmatch模块。比如:
      * import glob
      #
      * pyfiles = glob.glob('somedir/*.py')
      * from fnmatch import fnmatch
      #
      * pyfiles = [name for name in os.listdir('somedir')
      *            if fnmatch(name, '*.py')]


