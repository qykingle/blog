---
title: 算法笔记-c/c++快速入门
date: 2017-03-31 13:39:53
tags: [算法笔记, c/c++]
---
## c/c++快速入门
1. 在C++标准中，stdio.h更为推荐的等价方法是：cstdio
2. 绝对值在10^9范围内的整数都可以定义成int型，否则用long long，在初值后需要加上LL
3. 尽量使用double来存储浮点型数据
4. 0-9：48-57，A-Z: 65-90，a-z: 97-122
5. #define pi 3.14,末尾不加分号，但更推荐const double pi = 3.14， = acos(-1)
6. 位运算符没有算术运算符高
7. 除了%c外，scanf对其他格式符的输入是以空白符（空格，换行等）为结束标志
8. printf,%0md,不足位前面补充0
9. typedef long long LL; //给long long起一个别名LL
10. fabs(), pow(), floor(), ceil(),sqrt(),round()四舍五入
11. 数组的大小必须是整数常亮，不能是变量
12. 如果数组大小较大（大概10^6），则需要将其定义在主函数外面
13. 对于scanf，%c格式能够识别空格跟换行并将其输入，而%s通过空格或换行来识别一个字符串的结束
14. gets识别\n作为结束
15. string.h: strlen(), strcmp(), strcpy(), strcat()
16. sscanf(str, "%d", &n);从左读到右，sprintf(str, "%d", n);从右读到左
17. 数组第二维度必须定义
18. 两个int型的指针相减，等价于在求两个指针之间相差了几个int
19. 指针是一个unsigned的整数，引用是产生变量的别名，因此常量不可使用引用
20. 如果自己定义了构造函数，则不能不经过初始化就定义结构体变量
```c++
struct studentInfo {
    int id;
    char gender;
    //结构体的构造函数初始化
    studnetInfo(int _id, char _gender): id(_id), gender(_gender) {}
};
```
21. 浮点数的比较，引入极小的数进行修正，eps取1e-8基本上可以满足要求。
22. 一般的OJ系统，一秒钟的运算次数大概是10^7 ~ 10^8左右，因此O(n^2)的算法，n的规模为10000时是可以承受的。
