标准库：argparse

python命令行解析最简单最原始的方法时使用sys.argv 来实现
更高级的使用：argparse

要求：python2.7 以上

[root@zcheck-6 ~]# cat p2.py 
# -*- coding:utf-8 -*-

import argparse
# 导入argparse


if __name__ == '__main__':
    parse = argparse.ArgumentParser()
    # 创建解析器对象ArgumentParser
    parse.add_argument('-m', default='hello', help='world')
    # 用来指定程序可以接受的参数，此处表示只接受 -m
    parse.parse_args()
    # 从命令行中返回数据，此处是Namespace(m='hello')
    args = parse.parse_args()
    if args.m == 'hello':
        print('echo:hello')
    elif args.m == 'hi':
        print('echo:hi')
    else:
        print('not hello or hi')

# 执行
[root@zcheck-5 base_library_python]# python p2.py -h
usage: p2.py [-h] [-m M]

optional arguments:
  -h, --help  show this help message and exit
  -m M        world
[root@zcheck-5 base_library_python]# python p2.py -m aaaaa
Namespace(m='aaaaa')
not hello or hi
[root@zcheck-5 base_library_python]# python p2.py -m hello
Namespace(m='hello')
echo:hello
[root@zcheck-5 base_library_python]# python p2.py -m hi
Namespace(m='hi')
echo:hi
[root@zcheck-5 base_library_python]#

[root@zcheck-5 base_library_python]# cat p2.py 
# -*- coding:utf-8 -*-

import argparse


if __name__ == '__main__':
    parse = argparse.ArgumentParser()
    parse.add_argument('-m', '--mode', default='hello', help='world')
    # parse.add_argument('-m', default='hello', help='world')
    parse.parse_args()
    args = parse.parse_args()
    print(args)
    if args.m == 'hello':
        print('echo:hello')
    elif args.m == 'hi':
        print('echo:hi')
    else:
        print('not hello or hi')

# 当使用56行时，args.m 不能再使用，只能用 args.mode
[root@zcheck-5 base_library_python]# python p2.py -m hi
Namespace(mode='hi')
Traceback (most recent call last):
  File "p2.py", line 13, in <module>
    if args.m == 'hello':
AttributeError: 'Namespace' object has no attribute 'm'
[root@zcheck-5 base_library_python]#

[root@zcheck-5 base_library_python]# cat p2.py 
# -*- coding:utf-8 -*-

import argparse


if __name__ == '__main__':
    parse = argparse.ArgumentParser()
    parse.add_argument('-m', '--mode', default='hello', help='world')
    # parse.add_argument('-m', default='hello', help='world')
    parse.parse_args()
    args = parse.parse_args()
    print(args)
    if args.mode == 'hello':
        print('echo:hello')
    elif args.mode == 'hi':
        print('echo:hi')
    else:
        print('not hello or hi')

[root@zcheck-5 base_library_python]# python p2.py -m hi
Namespace(mode='hi')
echo:hi




