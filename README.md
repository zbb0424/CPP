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
 可以理解为编译单元的private，尽量让全局变量和函数用static标记，除非它们必须用在其他编译单元里
2.class/struct内  
 表示这部分的内存是这个类的所有实例共享的，即实例化n多个实体，但static变量只有一个；类里面的静态方法也一样，静态方法里没有该实例的指针this  
静态方法不能访问非静态变量  
静态局部变量的生命周期是整个程序，但作用域被限制

# 构造函数
c++构造函数必须手动初始化所有基础类型  
构造函数不会在没有实例化对象的时候运行，如果只调用静态方法，则不会运行构造函数  
如果不希望类被实例化可以把构造函数private，或者构造函数=delete；

# 虚函数
虚函数的成本：  
1.需要额外的内存储存虚表  
2.每次调用虚函数都需要遍历虚表  
纯虚函数=0  

# 数组
数组只是一个指针  
int example[5]  
如果直接打印这个数组，std::cout<<example<<std::endl; 只会打印这个数组的内存地址，因为它是一个指针  
如果要访问一个不存在数组中的索引，会造成内存访问冲突，因为我正在访问一个不属于我的内存  
数组中的数据是连续的，它们把数据放在了一行，我给五个整形分配了空间，意味着把他们一个接一个放进内存  
当我们通过特定的索引example[i]来访问时，这其实是对这段内存做了一个偏移  
在上面数组是一个指向包含5个整数的内存块的整形指针，这意味着可以创建一个整形指针类型变量，并把example赋值给它，例如int* ptr = example  
利用指针重写*（ptr+2）= 6,相当于给数组的第三个元素赋值为6  
  
为什么指针可以直接+2？  
处理指针时，只要在指针上加上像2这样的值，它会根据数据类型直接计算实际的字节数  
  
如何在堆上创建数组？
int* another = new int[5]，它和上面的意思相同，但生存周期不同。上面的创建在栈上，跳出作用域会被销毁，这个创建在堆上，它会存在到我们把它销毁或程序结束  
  
为什么要用new关键字来动态分配，而不是在栈上创建它们？  
最大的原因是生存期，因为new分配的内存会一直存在，直到你动手删除它  
另一件要考虑的是内存简介寻址，这意味着如果我们要访问这个数组，要在内存里跳来跳去，如果可以应该在栈上创建数组来避免这种情况，因为这样在内存跳跃肯定影响性能  
  
c++11中有标准库数组std::array，它有很多优点，边界检查，记录数组大小（我们没有办法知道上面的原生数组的大小）  
如果在栈上创建数组，例如上面的example，sizeof（example）得到的是这个数组实际占用多少字节（int4字节×5元素=20字节），int count = sizeof(example)/sizeof(int),count为元素数量  
但是如果用another做同样的事，得到的就会是一个整形指针的大小。4/4=1；所以这个技巧只能在栈分配的数组使用  


# 字符串  
字符串是字符数组  
c++原生字符串 const char* c++11开始必须加上const  
因为字符串不可变不可扩展，这是一个固定分配的内存块  
char* 不是在堆上分配的，所以不能delete  
字符串在内存是什么样的？如何工作？ 
通过ascii码存放的单独的字节，因为这是一个指针，要找出它的大小，所以以0结尾  
字符串从指针的内存地址开始，直到0结束  
std::string 本质上就是char数组加一些内置方法  
  
字符串字面量  
就是在双引号之间的字符，它的内容实际会变成什么取决于许多因素，最基本的情况下把鼠标悬停上面会发现他是一个const  char数组  

# const关键字  
const就是做出承诺某些东西是不会变的，不会改的  
const int* （int const*）常量指针：指针可以指向其他地址，但是指针所指向的地址的内容不能改变  
int* const 指针常量：可以改变所指向的地址的内容，但不能改变地址  

# 构造函数初始化列表  
在冒号后边的是初始化，大括号中的全部都只是赋值，所以引用类型必须在冒号后边写  

# 实例化  
c++中我们可以选择对象在哪里创建，是在堆上还是栈上  
栈对象有一个自动的生存周期  ，它们的生存周期由作用域确定，一旦超过作用域，它的内存就会被释放掉  
堆对象可以一直存在到程序结束，或者手动释放  
栈创建：Entity entity;缺点作用域小，内存空间可能不够  
堆创建：Entity* entity = new Entity();它返回了entity在堆上被分配的内存地址  
如果对象非常大，或者想控制对象的生存周期，在堆上创建；否则在栈上创建，更快自动回收  


