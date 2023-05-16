# C++如何工作
C++可以完全控制CPU执行的每一条指令  
有对应平台的编译器，C++可以在任何平台运行  

源文件-->compiling-->linking-->二进制文件（exe. lib）  
首先预处理#，这个过程发生在编译之前，头文件通过预处理被include在cpp中。cpp源文件被编译，每一个cpp编译为一个obj文件，然后通过链接器（linker）把obj联系起来组成二进制文件  
 
linker的工作就是联通各个函数  

# 变量
不同变量的唯一区别就是大小  
一个字节byte=8位bit  
一字（内存单元）=4字节（32位）或者8字节（64位）  
bool char 一字节  
int float 四字节  
double 八字节  
指针 32位4字节 64位8字节  

# 头文件
头文件声明，cpp定义
#pragma once头文件保护符，只在该翻译单元中include这个文件一次
另一种头文件保护符 #ifndef。。。#define。。。#endif

# 调试
内存视图：Debug->Windows->Memonry->Memonry1  
step into会进入当前函数F11   
step over转到当前函数下一行F10  
step out跳出当前函数shift+F11  

# 指针和引用
指针只是一个地址，一个int类型的内存地址
 ※B=&A B是A的地址  
引用本质上就是指针，引用是基于指针的语法糖，使代码更容易读写  
引用是对现有变量引用的另一种方式，相当于别名，引用变量并不真实存在  
int a=5;  
int& ref=a; ref并不存在
&取地址，※取内容  
一旦声明了一个引用，就不能修改它引用的对象  

# 静态static
c++的static根据上下文有两种意思  
1.class/struct外   
 link阶段是局部的，即只对定义它的编译单元（.obj）可见  
2.class/struct内  
 表示这部分的内存是这个类的所有实例共享的，即实例化n多个实体，但static变量只有一个；类里面的静态方法也一样，静态方法里没有该实例的指针this  
 
