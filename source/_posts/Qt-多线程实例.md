---
title: Qt多线程实例
date: 2019-10-08 13:28:06
tags: 
- Qt

categories: 
- YY
---

# 多线程实例

**使用QThread类，实现Qt多线程**

方法：使用一个类继承QThread，然后重新改写虚函数run()。



**使用moveToThread，实现Qt多线程**

通过这种方法不需要继承QThread,重写run()函数来实现Qt多线程，而是通过moveToThread(QThread *thread)函数将工作累对象移到所创建的QThread对象中去执行。利用信号与槽机制。

程序结构：
1.在主程序中，那里需要多线程就在哪里创建一个QThread实例；
2.把耗时操作封装到一个继承QObject的子类


