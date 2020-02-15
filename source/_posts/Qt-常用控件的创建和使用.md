---
title:  Qt常用控件的创建和使用
date: 2019-10-09 15:11:06
tags: 
- Qt

categories: 
- Qt
---

# 常用控件的创建和使用

``` C++
#include "mainwindow.h"
#include <QMenuBar>
#include <QToolBar>
#include <QPushButton>
#include <QStatusBar>
#include <QLabel>
#include <QDockWidget>
#include <QTextEdit>


MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
{
    this->resize(600,400);  //Set the window size

    QMenuBar *bar = menuBar();  //创建菜单栏,只能一个
    setMenuBar(bar);    //将菜单栏设置到窗口中

    QMenu * fileMenu = bar->addMenu("文件");
    QMenu * editMenu = bar->addMenu("编辑");


    //添加文件菜单项
    QAction * createAction = fileMenu->addAction("创建");
    fileMenu->addSeparator();//添加分割线
    QAction * closeAction = fileMenu->addAction("关闭");
    fileMenu->addSeparator();//添加分割线

    //添加编辑菜单栏
    QAction * copyAction = editMenu->addAction("拷贝");
    QAction * pasteAction = editMenu->addAction("粘贴");

    //菜单栏 可以有很多个
    QToolBar *toolBar = new QToolBar(this);
    //将工具栏放入窗口中
    addToolBar(Qt::LeftToolBarArea, toolBar);

    //只允许左右停靠
    toolBar->setAllowedAreas(Qt::LeftToolBarArea | Qt::RightToolBarArea
                             | Qt::TopToolBarArea | Qt::BottomToolBarArea);
    //设置是否允许浮动
    toolBar->setFloatable(false);
    //设置是否允许移动
    toolBar->setMovable(true);

    //在工具栏中添加控件
    QPushButton *btn = new QPushButton("按钮1",this);
    QPushButton *btn1 = new QPushButton("按钮2",this);
    btn1->setStyleSheet("QPushButton{color:red}");
    QPushButton *btn2 = new QPushButton("按钮3",this);

    toolBar->addWidget(btn);
    toolBar->addSeparator();
    toolBar->addWidget(btn1);
    toolBar->addSeparator();
    toolBar->addWidget(btn2);

    //状态栏，只有一个
    QStatusBar * status = statusBar();
    //将状态栏放入到窗口中
    setStatusBar(status);

    //创建标签
    QLabel * label1 = new QLabel("左侧信息", this);
    //将label放入到状态栏中
    status->addWidget(label1);
    QLabel * label2 = new QLabel("右侧信息", this);
    status->addPermanentWidget(label2);

    //铆接部件 浮动窗口 可以多个
    QDockWidget * dock = new QDockWidget("铆接部件", this);
    //将铆接部件放到窗体的核心部件的下方
    addDockWidget(Qt::BottomDockWidgetArea, dock);
    //铆接部件设置停靠范文
    dock->setAllowedAreas(Qt::TopDockWidgetArea | Qt::BottomDockWidgetArea);

    //创建核心部件 只能有一个
    QTextEdit * edit = new QTextEdit(this);
    //将文本编辑 放到窗体中间
    setCentralWidget(edit);
}

MainWindow::~MainWindow()
{

}
```

总结：直接使用set方法的窗口中只能有一个，使用add方法的窗口中可以有很多个
