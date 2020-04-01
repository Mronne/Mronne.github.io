---
layout: article
title: C++ primer plus（二）简单数据类型
tag: [Cpp,Cpp primer plus]
excerpt: C++ primer plus 中的简单数据类型
---

# 整型

## 宽度
- 宽度(width)用于描述存储整数时使用的内存量。
- 字节（byte）通常指的是8位的内存单元。
- 可以通过sizeof判断类型所占的字节数。


## 创建符号常量
- 使用预处理器编译指令，在编译时查找文件中对应的变量将其替换为数字。
```
#define INT_MAX 32767
```
- C++中更好的创建符号常量的方法是使用const。

## 初始化
- C++ 11提供另一种初始化方法，大括号中不包含任何东西时将被初始化为0
```
int wrens(32);
int wrens = {24};
int wrens {24};
```

## 无符号类型
- 对于有符号整型，如果超越了限制，其值将为范围另一端的取值。

## 整型类型的选择
- 一般选择在范围内的所占内存最小的类型
- 仅当有大型整型数组时，才有必要使用short
  
## 整型字面值
- 如果第一位是1~9，则基数为10（十进制 DEC）
- 如果第一位是0，第二位为1~7，则基数为8（八进制 OCT）
- 如果前两位是0x或者0X，则基数为16（十六进制 HEX）

使用cout进行不同进制输出时
```
int num = 42;
cout << hex;
cout << num <<endl; //以十六进制输出
```
- 控制符hex实际是一条消息，告诉cout采用何种行为。

## C++ 确定整型类型
- 使用后缀表达特定类型
    - u或U表示unsigned int
    - ul表示unsigned long
    - L表示long
    - LL表示long long
- 值太大不能存储为int

## 转义字符
- 程序使用推个字符会将光标退到上一次输入的位置

<div style="text-align: center"><img src="https://cdn.jsdelivr.net/gh/Mronne/MarkDownImg/img/20200401183842.png"/></div>

## 其他
1. 以两个下划线或下划线和大写字母打头的名称保留给编译器使用。以一个下划线开头的名称用作全局标识符。
2. 'A'的ASCII码为65
3. 'a'的ASCII码为97
   
# const限定符
const相比于宏定义的好处
- 能够明确指定类型
- 可以使用C++的作用域规则将定以限制在特定的作用域中
- 可以将const用于更复杂的类型
- 在C++中还可以使用const值来声明数组的长度


# 浮点数
- float通常为32位，double通常为64位
- 默认定义的浮点常量属于double类型，如果希望常量为float类型，使用f或F后缀。
- 对于float，C++只保证6位有效位。

# 算术运算符
- 对于求模运算符，两个操作数必须都是整型，将该运算符用于浮点数将导致编译错误。
- 当两个运算符的优先级相同时，C++将看操作数的结合性是从左到右还是从右到左。

# 数值转换

- 整型提升：在计算表达式时，C++会将bool、char、unsigned char、signed char和short转为int，计算机使用这种类型时，运算速度最快

<div style="text-align: center"><img src="https://cdn.jsdelivr.net/gh/Mronne/MarkDownImg/img/20200401184816.png"/></div>

- 强制类型转换：强制类型转换不会修改变量本身，而是创建一个新的、指定类型的值
```
(typeName) value //C语言中的转换
typeName (value) //C++中的转换
```

## auto声明
- 显示声明变量时，使用auto的帮助并不大，反而会导致自动推断类型产生一些错误
- 在处理复杂类型时，使用自动类型推断可以减少代码量。
```
std::vector<double> scores;
std::vector<double>::iterator pv = scores.begin(); //C++ 98

std::vector<double> scores;
auto pv = scores.begin(); //C++ 11
```

# 问题
- 为什么C++有多种整型？
> 可以根据需要选择适当的类型。可以使用不同的类型来提高计算速度。

- C++提供了什么措施来防止超出整型的范围？
> C++没有提供自动防止超出整型限制的功能，可以使用头文件climits来确定限制情况。

- 下面两条语句是否等价？
```
char grade = 65;
char grade = 'A';
```
> 在使用ASCII码的系统上，他们是等价的。第二条语句还可用于其他编码的系统。65是一个int常量，而'A'是一个char常量。 

- 找出编码88表示的字符
```
char c = 88;
cout << c << endl;

cout.put(char(88));

cout << char(88) << endl;

cout << (char)88 << endl; 
```

- 将long值赋给float变量会导致舍入误差，将long值赋给double变量呢？将long long赋给double变量呢？
> 取决于两个类型的长度。如果long为4个字节，则没有损失。因为最大的long值为20亿，即有10位数。由于double提供了至少13位有效数字，因而不需要进行任何舍入。long long 类型可提供19位有效数字，超过了double保证的13位有效数字的精度。