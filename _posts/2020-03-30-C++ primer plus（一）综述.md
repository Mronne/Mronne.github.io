---
layout: article
title: C++ primer plus（一）综述
tag: [C++,C++ primer plus]
excerpt: C++ primer plus 读后感
---

## 预处理器
```
#include<iostream>
```
- 这是预处理器编译指令，在编译时自动运行，iostream文件的内容将取代程序中的代码行。原始文件没有被修改，而是将源代码和iostream组成一个复合文件，在编译的下一阶段使用该文件。

## 头文件
- C++ 中头文件命名约定为
 
<div style="text-align: center"><img src="https://cdn.jsdelivr.net/gh/Mronne/MarkDownImg/img/20200330210511.png"/></div>

## endl和\n的区别
- 二者都是用于换行
- **endl**确保程序继续运行时刷新输出（将其立即显示在屏幕上）
- 在有些系统中，使用 **\n** 有可能在输入信息后才会出现提示

## cin和cout
- cin将输入看作是流入程序的字符流
- cin是istream类的一个预定义对象，cout是ostream类的一个预定义对象

## 函数
- 函数原型：函数定义前的声明。原型结尾的分号表面它是一条依据，这使得它是一个原型，而不是函数头。如果省略分号，编译器将把这行代码解释为一个函数头，并要求接着提供函数体。函数调用中必须包含括号。
- main()函数一般要求返回0，此时可以将计算机操作系统看作调用程序，函数将返回值返回给操作系统。
## 其他
- C++ 中分号标识语句的结尾，通常可以在能够使用回车的地方使用空格
- C++中可以连续使用赋值运算符，赋值将从右往左进行
```
int a,b,c;
a = b = c = 1;
```

- Build和Make指编译项目中所有源代码文件的代码，这通常是一个递增过程
- Link指将编译后的源代码与所需的代码库结合起来
- using namespace std是指定程序的命名空间，可以使用该名称空间中的函数