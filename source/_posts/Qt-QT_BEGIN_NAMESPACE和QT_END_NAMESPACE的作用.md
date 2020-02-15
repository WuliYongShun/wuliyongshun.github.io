---
title:  Qt中QT_BEGIN_NAMESPACE与QT_END_NAMESPACE的作用
date: 2019-10-09 15:11:06
tags: 
- Qt

categories: 
- Qt
---

# Qt中QT_BEGIN_NAMESPACE与QT_END_NAMESPACE的作用

 QT_BEGIN_NAMESPACE其实就是个宏，以前Qt4是没有命令空间的，后来才加上的，编译Qt源码时会有选项，是否将这些类放到专用的Qt命令空间内，默认是没有的。这就出来问题了，为了统一，如果你的代码在默认没有Qt命令空间的SDK中编译，那你就不用在前面加上命令空间，反之则需要。

为了屏蔽上面这个差异，使得你的代码能在这两种情况下都进行编译，Qt就提供了QT_BEGIN_NAMESPACE宏，这样开发者就省的自己来用程序或宏进行处理了。

至于说该宏提升编译速度什么的，那是上述类的声明的作用，与Qt无关的（也即与该宏QT_BEGIN_NAMESPACE无关），若要大幅提升编译速度需要开启qt的预编译头文件，会另起章节解说，并附测试结果。

``` Qt
#ifndef PREVIEWWINDOW_H

#define PREVIEWWINDOW_H

#include <QMainWindow>

#if 0
// 方式一:
#include <QTextBrowser>
#endif

#if 0
// 方式二:    比方式一可轻微提升编译速度
class QTextBrowser;
#endif

#if 1
// 方式三:    编译速度与方式二一样，该宏用于自编译qt源码是否启动命令空间的补充
QT_BEGIN_NAMESPACE
class QTextBrowser;
QT_END_NAMESPACE

#endif

class PreviewWindow : public QMainWindow
{
    Q_OBJECT
public:
    explicit PreviewWindow(QWidget *parent = 0);

signals:

public slots:

};

#endif // PREVIEWWINDOW_H 
```

