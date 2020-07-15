### 一、基础知识

1. #### 变量初始化

     int  wrens(432);     to  432

     int  emus{7};    to 7

     int  rheas={12};  to  12

     int   emus{};    to  0

     int rheas={};    to 0

   数组初始化：  int  emus[7]= { };

2. #### 基本数据类型

   char  int   short  long float  double

3. #### 进制表示

   042  八进制表示

   0x42 十六进制表示 

   cout  <<hex;      cout << oct;    cout << det;

   上述三个语句用于修改显示，修改前原格式有效

4. #### c++确定常量类型

   - 数字带后缀，  L   UL   LL  ULL  f
   - 不带后缀，编译器自动使用几种类型中能存储该数的最小类型表示

5. #### 格式控制符

   \n  \b退格   \t水平制表符     \r    \v垂直制表符    \a振铃   \\'    \\\"    \\?

   cout<<"Enter code:_________\b\b\b\b\b\b\b\b";  打印下划线后光标退回首端，线此时不消失

   