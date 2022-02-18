---
title: 汇编语言 第一、二章 含检测点和实验一
date: 2021-09-08 02:39:05
categories:
- notes
tags:
---
第一章 基础知识
第二章 寄存器

<!--more-->

# 第一章 基础知识

## 1.1 机器语言

机器语言是很多机器指令的集合。**机器指令** 是一串**二进制数字**，它可以被转换成一系列高低电平，以此**驱动**计算机的各个**电子器件**。

每一种微处理器都有自己的机器指令集。

使用机器指令已经可以操作计算机了，但是它有一个无法解决的问题，或者说是我们人类自己的问题，那就是它太难记忆或者阅读了。如果让你理解这段代码，并尝试找出其中的 bug ，你会作何感想？

{% asset_img Snipaste_2021-09-06_07-11-35.png %}

我已经看到自己皱起的眉头了

这个问题需要解决，所以我们看看汇编语言的产生



## 1.2 汇编语言的产生

可以将汇编语言简单地理解为**机器语言**的**别名**或**外号**。我们在中学小学的时候很喜欢给同学起外号，因为外号叫起来更顺口。

汇编语言也是因此而生，它通过更容易阅读和理解的字母代替机器语言，等到要上机执行的时候，再通过一个叫做 **编译器** 的东西将它翻译成对应的 **机器语言** 执行。

整个过程如下图所示

{% asset_img Snipaste_2021-09-06_07-17-16.png %}



## 1.3 汇编语言的组成

* 汇编指令：机器指令的助记符，有对应的机器码
* 伪指令：给编译器用的，没有对应的机器码
* 其它的符号：+、-、*、/等，给编译器用的，没有对应的机器码

从各个部分的特点也能看出，汇编指令是汇编语言的核心



## 1.4 存储器

这里说的存储器指的是 **内存**（memory）



## 1.5 指令和数据

指令和数据在存储介质中没有任何区别，它们都是一串一串的二进制信息。

它们的不同之处在 CPU 中得到体现。CPU把有的信息看作指令，有的信息看作数据。



## 1.6 存储单元

## 1.7 CPU对存储器的读写

首先我们应该考虑到，一台计算机中除了CPU和内存之外，还有其它的器件。所以如果 想对内存进行读写，首先要给出一个信息指定我们要操作的器件（控制信息）。OK，给出控制信息后，我们只要指定想要操作的 存储单元的地址（地址信息） 和 对应的数据（数据信息） 就可以读写内存了。

那么 这些信息又是怎么在各个器件之间进行传输的呢？

电信号。计算机内的信息都是通过电信号传输的，自然，传输介质就是**导线**了。 但是我们一般不把它们叫做导线，而叫做 **总线**。根据传输信号的类型不同，又把它们分为 **控制总线**、**地址总线**和**数据总线**。



## 1.8 地址总线

宽度为 $N$ 的地址总线能够寻址 $2^N$ 个地址单元



## 1.9 数据总线

负责在CPU和其它器件之间传输数据

数据总线的宽度决定了CPU和外界**数据传送**的**速度**



## 1.10 控制总线

控制总线的宽度决定了CPU对外部器件的**控制能力**



## 检测点 1.1

* 1个CPU的寻址能力为 8KB ，那么它的地址总线的宽度为 $log_22^{13}=13$ 位
* 1KB 的存储器有 $1024$ 个存储单元。存储单元的编号从 $0$ 到 $1023$
* 1KB 的存储器可以存储 $2^10=1024$ 个Byte，$2^3*2^{10}=8192$ 个 Bit
* 1GB、1MB、1KB 分别是 $2^{30},\ 2^{20}, \ 2^{10}$ 个 byte
* 地址总线宽度为 16 根、20根、24根、32根的CPU的寻址能力分别为 64KB、1MB、16MB、4GB
* 数据总线宽度为 8根、16根、32根 的CPU一次可以传送的数据为 1byte、2byte、4byte
* 从内存中读取1024byte 的数据，8086 CPU（数据总线宽度为16 根）至少要读 $\frac{1024}{2}=512$ 次，80386 CPU（数据总线宽度为32 根）至少要读 $\frac{1024}{4}=256$​ 次
* 在存储器中，数据和程序以 **二进制** 形式存放



## 1.11 内存地址空间



## 1.12 主板

主板是计算机各种器件的家



## 1.13 接口卡

在计算机系统中，CPU不能直接控制外部设备（显示器、音箱、打印机等）。但是CPU可以通过总线向接口卡发送命令，接口卡根据CPU的命令控制外部设备的工作。



## 1.14 各类存储器芯片

BIOS (Basic Input/Output System)



## 1.15 内存地址空间

一个计算机系统中可以有多个不同的存储器，但是CPU把它们看作一个整体，即逻辑存储器。不同的存储器占据逻辑存储器的不同部分。如下图所示

{% asset_img Snipaste_2021-09-06_15-13-54.png %}

这个假想的逻辑存储器也叫做 **内存地址空间**



# 第二章 寄存器

这里说的寄存器是在**CPU内部**的寄存器，它用来**保存**CPU运算单元要用到的**数据**

## 2.1 通用寄存器

用来存放一般性数据的寄存器称作通用寄存器。比如8086CPU中的 AX 、BX 、CX 、DX 寄存器，而且它们都是**16位**通用寄存器

 

## 2.2 字（word）在寄存器中的存储



## 2.3 几条汇编指令

首先，汇编指令和寄存器名称**不区分**大小写

下图展示了 `mov` 和 `add` 两种指令

{% asset_img Snipaste_2021-09-07_07-36-28.png %}

进行数据传送或者运算的时候要注意指令的两个操作对象的**位数应该一致**



## 检测点 2.1

1. 写出每条汇编指令执行后相关寄存器中的值

   ```assembly
   mov ax,62627		# AX=F4A3H
   mov ah,31H			# AX=31A3H
   mov al,23H			# AX=3123H
   add ax,ax			# AX=6246H
   mov bx,826CH		# BX=826CH
   mov cx,ax			# CX=6246H
   mov ax,bx			# AX=826CH
   add ax,bx			# AX=04D8H
   mov al,bh			# AX=0482H
   mov ah,bl			# AX=6C82H
   add ah,ah			# AX=D882H
   add al,6			# AX=D888H
   add al,al			# AX=D810H
   mov ax,cx			# AX=6246H
   ```

   

2. 使用且最多使用4条目前学过的指令计算 $2^4$ 

   ```assembly
   mov ax,2
   add ax,ax
   add ax,ax
   add ax,ax
   ```

   



## 2.4 物理地址

内存单元的**唯一**地址



## 2.5 16位结构的CPU

16位结构包含这几个特性：

* 运算器一次最多处理16位的数据
* 寄存器的最大宽度为16位
* 寄存器和运算器之间的通路为16位



8086 是 16位结构的CPU



## 2.6 8086CPU 给出物理地址的方法

8086CPU 的地址总线宽度为 20 位，有1MB的寻址能力。

但是8086CPU 内部是16位结构，如果直接从内部发出地址就只有16位，寻址能力只有 64KB 

所以8086CPU 采用了一种在内部用两个16位地址**合成**的方法来形成一个20位的物理地址

{% asset_img Snipaste_2021-09-07_15-38-13.png %}

如上图所示，当8086CPU读写内存时

1. CPU提供两个16位地址，一个**段地址**，一个**偏移地址**
2. 段地址和偏移地址通过内部总线送入 **地址加法器**
3. 地址加法器将 两个 16 位地址合成为一个 20 位**物理地址**
4. 地址加法器将物理地址送入**输入输出控制电路**
5. 物理地址被送入**地址总线**，通过总线到达存储器



物理地址是怎么合成的呢？

**物理地址= 段地址 $\times$ 16 + 偏移地址**



## 2.7 物理地址= 段地址 $\times$ 16 + 偏移地址 的本质含义

CPU在访问内存时，用一个**基础地址**和一个相对于基础地址的**偏移地址**相加 得到内存单元的 物理地址



## 2.8 段的概念

段的概念仅仅存在于CPU中，而实际的物理存储器并没有分段



## 检测点 2.2 

1. 给定段地址为 0001H ，仅通过变化偏移地址寻址，CPU的寻址范围为 00010H 到 1000FH
2. 有一数据存放在内存 20000H 单元中，现给定段地址为SA，若想用偏移地址寻到此单元。则SA应满足的条件是：最小为 1001H ，最大为 2000H



## 2.9 段寄存器

8086CPU中专门使用四个 **段寄存器** 给出 段地址

这里只看一个，CS



## 2.10 CS 和 IP

8086CPU中两个非常重要的寄存器

在任意时刻，设CS中的内容为M，IP中的内容为N，则8086CPU将从内存 $M \times 16+N$ 单元开始，读取一条指令并执行

在8086CPU 加电启动或者复位后，CS 和 IP 被设置为CS=FFFFH，IP=0000H。所以在 8086CPU 机器刚刚启动时，CPU从内存FFFF0H 单元中读取指令执行



## 2.11 修改 CS、IP的指令

既然CS和IP寄存器指定了CPU接下来要执行的指令，那么我们就可以修改这两个寄存器的值来执行我们想要执行的指令

使用 8086CPU 时不能通过 `mov` 指令修改CS和IP寄存器的值，但是它提供了一系列**转移指令**来完成这项工作

最简单的转移指令是 `jmp` 

如果同时改变CS和IP的值 则 `jmp 段地址：偏移地址`，执行完毕后，CS=指定段地址，IP=指定偏移地址

如果只改变IP的值 则 `jmp 某一寄存器` ，执行完毕后，IP的值=指定寄存器内存储的值



## 2.12 代码段

用来存放代码的一段内存



## 检测点 2.3

下面的3条指令执行后，CPU几次修改IP？都是在什么时候？最后IP中的值是多少？

```assembly
mov ax,bx		# 第一次修改
sub ax,ax		# 第二次修改
jmp ax			# 第三、第四次修改，最后IP中的值是 ax 寄存器中的值 0000H
```





# 实验一 查看CPU和内存，用机器指令和汇编指令编程

Debug 功能

* R 查看、改变CPU寄存器的内容

* D 查看**内存**中的内容

  `d 段地址：偏移地址` 查看内存中指定地址处的内容

  `d 段地址：偏移地址 结尾偏移地址`  查看内存中指定范围内的内容

  

* E 改写**内存**中的内容

  `e 起始地址 数据 数据 数据 ……` 修改内存中从 起始地址开始的 n 个单元的内容

  

* U 将**内存**中的机器指令 **翻译成** 汇编指令

  `u 段地址：偏移地址` 将指定地址开始的机器指令翻译成汇编指令并显示出来

  

* T 执行一条机器指令

  执行的是 CS:IP 地址处的指令

  

* A 以**汇编**指令的格式在内存中写入一条机器指令

  

## 实验任务

1. 使用 debug 将下面的程序段写入内存，逐条执行，观察每条指令执行后CPU中相关寄存器内容的变化

   ```assembly
   mov ax,4E20H
   add ax,1416H
   mov bx,2000H
   add ax,bx
   mov bx,ax
   add ax,bx
   mov ax,001AH
   mov bx,0026H
   add al,b1
   add ah,b1
   add bh,al
   mov ah,0
   add al,b1
   add al,9CH
   ```

   使用 A 命令输入：

   {% asset_img Snipaste_2021-09-07_21-08-10.png %}

   使用 T 命令执行：

   {% asset_img Snipaste_2021-09-07_21-10-45.png %}

   {% asset_img Snipaste_2021-09-07_21-12-02.png %}

   {% asset_img Snipaste_2021-09-07_21-12-50.png %}

   {% asset_img Snipaste_2021-09-07_21-13-13.png %}

   

2. 将下面3条指令写入从 2000:0 开始的内存单元中，利用这3条指令计算 $2^8$​​ 

   ```shell
   mov ax,1
   add ax,ax
   jmp 2000:0003
   ```

   写入：

   {% asset_img Snipaste_2021-09-07_21-16-12.png %}

   执行：

   {% asset_img Snipaste_2021-09-07_21-17-13.png %}

   {% asset_img Snipaste_2021-09-07_21-18-15.png %}

   {% asset_img Snipaste_2021-09-07_21-19-52.png %}

3. 查看内存中的内容

   PC机主板的 ROM 中写有一个生产日期，在内存 FFF00H~FFFFFH 的某几个单元中，请找到这个生产日期并试图改变它

    首先寻找目标：

   {% asset_img Snipaste_2021-09-07_21-23-18.png %}

   试图把 修改日期

   {% asset_img Snipaste_2021-09-07_21-26-43.png %}

   结果证明，这块内存是**不能被改变**的

4. 向内存从 B8100H 开始的单元中填写数据

   ```shell
   -e B810:0000 01 01 02 02 03 03 04 04
   ```

   先填写不同的数据，观察产生的现象；再改变填写的地址，观察现象

{% asset_img Snipaste_2021-09-07_21-28-58.png %}

第一次修改失败了，换个数据试试

{% asset_img Snipaste_2021-09-07_21-30-06.png %}

又失败了

当我把 B810:0000 周围的内容都显示出来的时候，又出现了不一样的现象

{% asset_img Snipaste_2021-09-07_21-36-06.png %}

查看同一段地址的内容，两次的结果竟然不一样

查了几条帖子，原来这个地址是**显存**，每次查看内存内容的时候要显示的东西都不一样，显存内容自然也就不一样了
