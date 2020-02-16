---
title: C-回调函数
date: 2020-02-16 21:41:38
tags:
- C

categories:
- YY
---

# 回调函数(Callback Functions)

回调函数就是一个通过**函数指针**调用的函数。如果你把函数的指针（地址）作为参数传递给另一个函数，当这个指针被用来调用其所指向的函数时，我们就说这是回调函数。*回调函数不是由该函数的实现方直接调用，而是在特定的事件或条件发生时由另外的一方调用的，*用于对该事件或条件进行响应。

 来自Stack Overflow某位大神简洁明了的表述：A "callback" is any function that is called  by another function which takes the first function as a parameter。  也就是说，函数 F1 调用函数 F2 的时候，函数 F1 通过参数给 函数 F2 传递了另外一个函数 F3 的指针，在函数 F2  执行的过程中，函数F2 调用了函数 F3，这个动作就叫做回调（Callback），而先被当做指针传入、后面又被回调的函数 F3  就是回调函数。到此应该明白回调函数的定义了吧？ 

## 使用回调函数的好处
回掉函数的好处和作用，那就是解耦，就是因为这个特点，普通函数代替不了回调函数。所以，在我眼里，这才是回调函数最大的特点。来看看维基百科上面我觉得画得很好的一张图片。
***
<img src="I:\ShunWork\Myblog\source\_posts\PICTURE\2417.jpg" alt="calback picture" style="zoom:80%;" />
***

**C语言代码举例说明以上图片**

```c
#include<stdio.h>
#include<softwareLib.h> // 包含Library Function所在读得Software library库的头文件
 
int Callback() // Callback Function
{
	// TODO
	return 0;
}
 
int main() // Main program
{
	// TODO
	Library(Callback);
	// TODO
	return 0;
}
```

*乍一看，回调似乎只是函数间的调用，和普通函数调用没啥区别，但仔细一看，可以发现两者之间的一个关键的不同：在回调中，主程序把回调函数像参数一样传入库函数。这样一来，只要我们改变传进库函数的参数，就可以实现不同的功能，这样有没有觉得很灵活？并且丝毫不需要修改库函数的实现，这就是解耦。再仔细看看，主函数和回调函数是在同一层的，而库函数在另外一层，想一想，如果库函数对我们不可见，我们修改不了库函数的实现，也就是说不能通过修改库函数让库函数调用普通函数那样实现，那我们就只能通过传入不同的回调函数了，这也就是在日常工作中常见的况。现在再把main()、Library()和Callback()函数套回前面 F1、F2和F3函数里面，是不是就更明白了？*

## 怎么使用回调函数？
**举例如下：**
```c
#include<stdio.h>

int Callback_1() // Callback Function 1
{
    printf("Hello, this is Callback_1 ");
    return 0;
}

int Callback_2() // Callback Function 2
{
    printf("Hello, this is Callback_2 ");
    return 0;
}

int Callback_3() // Callback Function 3
{
    printf("Hello, this is Callback_3 ");
    return 0;
}

int Handle(int (*Callback)())
{
    printf("Entering Handle Function. ");
    Callback();
    printf("Leaving Handle Function. ");
}

int main()
{
    printf("Entering Main Function. ");
    Handle(Callback_1);
    Handle(Callback_2);
    Handle(Callback_3);
    printf("Leaving Main Function. ");
    return 0;
}
```

运行结果：
***
```
Entering Main Function.
Entering Handle Function.
Hello, this is Callback_1
Leaving Handle Function.
Entering Handle Function.
Hello, this is Callback_2
Leaving Handle Function.
Entering Handle Function.
Hello, this is Callback_3
Leaving Handle Function.
Leaving Main Function.
```
***
*可以看到，Handle()函数里面的参数是一个指针，在main()函数里调用Handle()函数的时候，给它传入了函数Callback_1()/Callback_2()/Callback_3()的函数名，这时候的函数名就是对应函数的指针，也就是说，回调函数其实就是函数指针的一种用法。现在再读一遍这句话：A "callback" is any function that is called by another function which  takes the first function as a parameter，是不是就更明白了呢？*

## 带参数的回调函数的使用
```c
#include<stdio.h>

int Callback_1(int x) // Callback Function 1
{
    printf("Hello, this is Callback_1: x = %d ", x);
    return 0;
}

int Callback_2(int x) // Callback Function 2
{
    printf("Hello, this is Callback_2: x = %d ", x);
    return 0;
}

int Callback_3(int x) // Callback Function 3
{
    printf("Hello, this is Callback_3: x = %d ", x);
    return 0;
}

int Handle(int y, int (*Callback)(int))
{
    printf("Entering Handle Function. ");
    Callback(y);
    printf("Leaving Handle Function. ");
}

int main()
{
    int a = 2;
    int b = 4;
    int c = 6;

    printf("Entering Main Function. ");
    Handle(a, Callback_1);
    Handle(b, Callback_2);
    Handle(c, Callback_3);
    printf("Leaving Main Function. ");
    return 0;
}
```
运行结果：
***
```
Entering Main Function.
Entering Handle Function.
Hello, this is Callback_1: x = 2
Leaving Handle Function.
Entering Handle Function.
Hello, this is Callback_2: x = 4
Leaving Handle Function.
Entering Handle Function.
Hello, this is Callback_3: x = 6
Leaving Handle Function.
Leaving Main Function.
```
***
*可以看到，并不是直接把int Handle(int (*Callback)()) 改成 int Handle(int (*Callback)(int)) 就可以的，而是通过另外增加一个参数来保存回调函数的参数值，像这里 int Handle(int y, int (*Callback)(int)) 的参数 y。同理，可以使用多个参数的回调函数。*

***

