---
title:  Qt中C++中文显示
date: 2019-10-09 15:11:06
tags: 
- C++
- Qt

categories: 
- YY
---
# Qt中C++中文显示


```C++
#include <QTextCodec>    //1.包含头文件

QTextCodec *codec;     //2声明一个全局变量
codec = QtextCodec::codecForName("GBK");    //将编码格式声明为GBK
ui->textEdit->setText(codec->toUnicode*("中文"));    //将中文转换为为固定编码格式
```