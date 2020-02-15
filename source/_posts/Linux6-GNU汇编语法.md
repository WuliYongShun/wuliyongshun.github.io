---
title: Linux6-GNU汇编语法
date: 2020-02-05 16:01:06
tags:
- Linux

categories:
- Embedded system

---

# GNU汇编

GNU 汇编语法适用于所有的架构，并不是 ARM 独享的， GNU 汇编由一系列的语句组成，每行一条语句，每条语句有三个可选部分，如下：
```
label: instruction @ comment
```
***lavel*** 即标号，表示地址位置，有些指令前面可能会有标号，这样就可以通过这个标号得到指令单的地址，标号也可以用来表示数据地址。注意label后面的冒号“：”，任何以冒号“：”结尾的标识符都会被认识是一个标号。

***instruction*** 即指令，也就是汇编指令或伪指令。

***@*** 标号，表示后面是注释，就跟C语言里面的“/*   */“一样，其实在GNU汇编文件中我们可以使用同样的来进行注释。

***comment*** 就是注释内容。

比如如下代码：

```
add:
	MOVS R0,#0X12 @设置 R0=0X12
```

  上面代码中“add:”就是标号，“MOVS R0,#0X12”就是指令，最后的“@设置 R0=0X12”就是注释。

 ***注意！* **ARM 中的指令、伪指令、伪操作、寄存器名等可以全部使用大写，也可以全部使用小写，但是不能大小写混用。  

 

用户可以使用.section伪操作来定义一个段，汇编系统预定义了一些段名:

***.text*** 表示代码段。

***.data*** 初始化的数据段。

***.bss*** 为初始化的数据段。

***.rodata*** 只读数据段。

​	我们当然可以自己使用.section来定义一个段，每个段以段名开始，以下一段名或者文件结尾结束，比如：

```
.section .testsection @定义一个testsection段
```

汇编程序的默认入口标号是_start，不过我们也可以在链接脚本中使用ENTRY来指明其它 的入口点，下面的代码就是使用_start 作为入口标号：
```
.global _start

_start
	ldr r0, =0x12 @r0=0x12
```
上面代码中.global是伪操作，表示_start是一个全局标号，类似C语言里面的全局变量一样，常见的伪操作有：
***.byte*** 定义单字节数据，比如.byte 0x12。
***.short*** 定义双字节数据，比如.byte 0x1234。
***.long*** 定义一个4字节数据，比如.long 0x12345678。
***.equ*** 赋值语句，格式为： .equ 变量名，表达式，比如.equ num,0x12，表示 num = 0x12。
***.align*** 数据字节对齐，比如：.align 4表示4字节对齐。
***.end*** 表示源文件结束。
***.global*** 定义一个全局符号，格式为： .global symbol, 比如： .global _start


## GNU 汇编同样也支持函数，函数格式如下：
```
函数名：
	函数体
	返回语句
```
GNU汇编函数返回语句不是必须的，如下代码就是用汇编写的Cortex-A7中断服务函数：
```
/* 未定义中断 */
Undefined_Handler:
	ldr r0, = Undefined_Handler
	bx r0
	
/* SVC中断 */
SVC_Handler:
	ldr r0, =SVC_Handler
	bx r0
	
/* 预取终止中断 */
PrefAbort_Handler:
	ldr r0, =PrefAbort_Handler
	bx r0
```

上述代码中定义了三个汇编函数： Undefined_Handler、 SVC_Handler 和PrefAbort_Handler。以函数 Undefined_Handler 为例我们来看一下汇编函数组成，“Undefined_Handler”就是函数名，“ldr r0, =Undefined_Handler”是函数体，“bx r0”是函数返回语句，“bx”指令是返回指令，函数返回语句不是必须的。

# Cortex-A7常用汇编指令
所有汇编指令请参考《ARM ArchitectureReference Manual ARMv7-A and ARMv7-R edition.pdf》的 A4章节。

## 1.处理器内部数据传输指令
使用处理器做的最多的事情就是在树立起内部来回的传递数据，常见的操作有：

















