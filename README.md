# C++如何工作
C++可以完全控制CPU执行的每一条指令  
有对应平台的编译器，C++可以在任何平台运行  

源文件-->compiling-->linking-->二进制文件（exe. lib）  
首先预处理#，这个过程发生在编译之前，头文件通过预处理被include在cpp中。cpp源文件被编译，每一个cpp编译为一个obj文件，然后通过链接器（linker）把obj联系起来组成二进制文件  
 
linker的工作就是联通各个函数  

# 变量
不同变量的唯一区别就是大小

# 头文件
头文件声明，cpp定义
#pragma once头文件保护符，只在该翻译单元中include这个文件一次
另一种头文件保护符 #ifndef。。。#define。。。#endif

