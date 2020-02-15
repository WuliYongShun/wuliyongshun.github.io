---
title:  C++中显式、隐式与explicit关键字
date: 2019-10-09 15:11:06
tags: 
- C++

categories: 
- YY
---
# C++中显式、隐式与explicit关键字

***1.隐式转换***
隐式转换，即编译器完成的转换，例如
int a = 1;
float b = 3;
float sum;
sum = a + b;//a是int类型，b是float类型；在编译的时候，编译器自动将int a转换成了float类型

***2.显式转换***
显式转换，即用户完成的转换，例如
float a = 1;
float b = 3;
int s;
s = (int)a + (int)b;//float类型的a与b被显示的(强制)转换成成为float数据类型

对于非数据的函数函数而言，例：
``` C++
#include <iostream>
using namespace std;

class A{
　　int x;
　　public:
　　　　A(){x=0;cout<<"Create A:0"<<endl;}
　　　　A(int a){x=a;cout<<"Create A:"<<x<<endl;}
　　　　~A(){cout<<"Delete A:"<<x<<endl;}
};
void main()
{
　　A a1;
　　A *a2=new A(10);
　　delete a2;
}
```
程序分析：
A a1；隐式的调用了A();
A *a2 = new A(10);对A()进行了重载，显式的调用了A(int a);

***3.explicit关键字***

explicit用于构造函数，抑制隐式转换的发生，防止出现误区。








