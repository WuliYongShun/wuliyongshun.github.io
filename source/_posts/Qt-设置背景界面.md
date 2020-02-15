---
title:  Qt设置背景界面
date: 2019-10-09 15:11:06
tags: 
- Qt

categories: 
- Qt
---

# Qt设置背景界面

1.设置背景图片的一种方式

```C++
QPixmap pixmap(QString::fromUtf8("./icon/background.png"));//当前文件夹下面的图片
QPalette palette = this->palette();
palette.setBrush(backgroundRole(), QBrush(pixmap));
setPalette(palette);
```


2.使用Qt捕获windows窗口变化事件函数，自动调整背景缩放

``` C++
void （当前函数所在类）::resizeEvent(QResizeEvent *e)
{
    Q_UNUSED(e);    //不使用传入参数e，避免警告
    int w = this->widght();    //w为当前widght宽度
    int h = this->height();    //h为当前widght高度
    QPixmap back_icon(QString::fromUtf8("资源路径"))；    //back_icon指向图片路径
    QPlette.setBrush(this->backgroundRole(),QBrush(back_icon.scaled(w,h)));    //设置窗体背景和和缩放比例
    this->setPalette(palette);    //设置当前palette生效
}
```