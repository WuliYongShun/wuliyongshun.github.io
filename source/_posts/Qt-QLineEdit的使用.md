---
title:  Qt中QLineEdit的使用
date: 2019-10-09 15:11:06
tags: 
- Qt

categories: 
- YY
---
# QLineEdit的使用

定义：
        QLineEdit是一个单行文本编辑控件。
功能：
        可以调用多个可用函数，输入和编辑单行文本，比如撤销、恢复、剪切、粘贴及拖放等。

函数说明：
    echoMode()：可以设置其属性，比如一密码的形式输入；
    maxLength()：限制文本长度；
    validator()或inputMask()：限制智能输入数字，在对同一个QLineEdit的validator或者inputmask进行转换时，最好将它的validator或者inputmask清楚，以避免错误发生；

与QLineEdit相关的一个类QTextEdit，她允许多行文本以及富文本编辑：
    setText()或者insert()改变其中的文本;
    text()：获得文本；
    displayText()：获得显示的文本；
    setSelection()或者selectAll()选中文本；
    cut()、copy()、paste()函数可以对文本中的数据进行剪切、复制和粘贴；
    setAlignment()：设置文本为位置；

信号反馈：
    文本改变信号：textChange();
    不是由setText()造成文本的改变信号：textEdit();
    鼠标光标改变时信号：cursorPostionChanged()；
    返回键或者回车键按下时信号：returnPressed();

常用方法说明：

1.setPlaceholderText()设置提示文字
![文本框提示文字](https://images2015.cnblogs.com/blog/628412/201602/628412-20160205204407710-892374169.jpg)
豆瓣电影的搜索输入框，没有输入任何字符时，显示“电影、影人、影院、电视剧”这些占位文字，对用户输入作相关提示。
echoLineEdit->setPlaceholderText("电影、影人、影院、电视剧");

2.setEchoMode()设置模式
![淘宝](https://images2015.cnblogs.com/blog/628412/201602/628412-20160205223926663-818638865.jpg)
淘宝登录界面的一部分，用户名可以直接看到，密码一般都用小黑点掩盖。
```Qt
switch(index)
{
    case 0:
            //默认,输入什么即显示什么
            echoLineEdit->setEchoMode(QLineEdit::Normal);
            break;
     case 1:
             //密码，一般用小黑点覆盖你所输入的字符
             echoLineEdit->setEchoMode(QLineEdit::Password);
             break;
    case 2:
            //编辑时输入字符显示输入内容否则用小黑点代替
            echoLineEdit->setEchoMode(QLintEdit::PasswordEchoOnEdit);
            break;
    case 3:
            //任何输入都看不见（只是看不见，不是不能输入）
            echoLineEdit->setEchoMode(ALineEdit::NoEcho);
}
```

3.setAlignment()设置文本位置
``` C++
switch(index)
{
    case 0:
            alignmentLineEdit->setAlignment(Qt::Alignleft);
            break;
    case 1:
            alignmentLineEdit->setAlignment(Qt::AlignCenter);
            break;
    case 2:
            alignmentLineEdit->setAlignment(Qt::AlignRight);
}
```

4.setReadOnly()设置能否编辑
``` C++
switch(index)
{
    case 0:
            accessLineEdit->setReadOnly(false);
            break;
    case 1:
            accessLineEdit->setReadOnly(true);
}
```

5.setValidator()对输入进行限制
这种方式的是指是通过正则表达式限制输入内容
![输入限制](https://images2015.cnblogs.com/blog/628412/201602/628412-20160205224628272-1758708857.jpg)
``` Qt
switch(index)
{
    case 0:
            //无限制
            validatorLineEdit->setValidator(0);
            break;
    case 1:
            //只能输入整数
            validatorLineEdit->setValidator(new QintValidator);
            break;
    case 2:
            //实例，只能输入-180到180之间的小数，小数点后最多两位（可用于限制经纬度等）
            QDoubleValodator *pDfValidator = new QDoubleValidator(-180, 180.0, 2, validatorLineEdit);
            pDfValidator->setNotation(QDoubleValidator::StandardNotation);
            validatorLineEdit->setValidator(pDfValidator);
}
```

6.setInputMask()对输入进行限制
通过限制格式限制输入，具体怎么格式化客气参考Qt助手。
![对输入进行限制](https://images2015.cnblogs.com/blog/628412/201602/628412-20160205213813663-1721525219.jpg)
``` Qt
switch(index)
{
    case 0:
            inputMaskLineEdit->setInputMask("");
            break;
    case 1:
            inputMaskLineEdit->setInputMask("-99 99 99 99 99;_");
            break;
    case 2:
            inputMaskLineEdit->setInputMask("0000-00-00");
            inputMaskLineEdit->setText("00000000");
            inputMaskLineEdit->setCursorposition(0);
            break;
    case 3:
            inputMaskLineEdit->setInputMask(">AAAAA-AAAAA-AAAAA-AAAAA-AAAAA;#");
}
```

7.setLength()设置可以输入的最多字符数
//最多只能输入9个字符
```
echoLineEdit->setMaxLength(9);
```

8.validator和inputmask的结合
比如经纬度用“度”

