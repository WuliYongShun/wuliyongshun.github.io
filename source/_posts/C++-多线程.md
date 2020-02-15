---
title: C++多线程
date: 2019-10-09 15:11:06
tags: 
- C++
- Qt
categories: 
- YY
---
# 多线程

``` C++
CRITICAL_SECTION CriticalSection;    //防止共有资源被同时调用
static int number = 10;    //定义一个变量初始值为10

DWORD WINAPI ThreadOne(LPVOID lpParameter)
{
    qDebug() << "窗口1开始售票";
    while(1)
    {
        EnterCriticalSection(&CriticalSection);    //进入临界状态
        if(number > 0)
        {
            qDebug() << "窗口1售出" << number;    //打印出线程1抢占数值
            number--;
            Sleep(1000);
       }
       LeaveCriticalSection(&CriticalSection);    //退出临界状态
       Sleep(100);
   }
   return 0;
}

DWORD WINAPI ThreadTwo(LPVOID lpParameter)
{
    qDebug() << "窗口2售票开始";
    while(1)
    {
    EnterCriticalSection(&CriticalSection);    //进入线程临界状态
    if(number>0)
    {
        qDebug() << "窗口2售出第" << number << "张票"；
        Sleep(1000);
        number--;
    }
    LeaveCriticalSection(&CriticalSection);
    Sleep(100);
    }
    return 0;
}

void Widget::on_pushButton_clicked()
{
    HANDLE HOne,HTwo;
    InitaializeCriticalSection(&CriticalSection);
    qDebug() << "*********vpoet******";
    HOne = CreateThread(NULL,0,ThreadOne,NULL,0,NULL);
    HTwo = CreateThread(NULL,0,ThreadTwo,NULL,0,NULL);
    CloseHandle(HOne);
    CloseHandle(HTwo);
    while(TRUE)
    {
        if(number = 0)
        {
            qDebug() << "票没了！"
            DeleCriticalSection(&CriticalSection);
            return;
        }
        else
        {
            coutinue;
        }
    }
    return;
}

```