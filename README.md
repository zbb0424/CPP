# C++如何工作
代码-->编译器compiler产生机器码（CPU的真正指令  
C++可以完全控制CPU执行的每一条指令  
有对应平台的编译器，C++可以在任何平台运行  

源文件-->编译器-->二进制文件（exe. lib）  
编译器收到源文件做的第一件事：预处理#所有预处理指令，这个过程发生在编译之前，头文件通过预处理被include在cpp中  
预处理之后，cpp源文件会被编译，编译器把cpp转为机器码，每个cpp文件被单独编译，每个cpp被编译为一个object文件，之后链接器（linker）需要把一个个obj联系起来，组成二进制文件（eg. exe）  
文件被编译后，linker回去找函数定义，然后和调用函数的位置联系起来，如果找不到定义，就会得到linker error  
linker的工作就是联通各个函数  
