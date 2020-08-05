---
title: C++剑指offer刷题（八）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-20 10:44:20
tags:
keywords: 位操作
description: 二进制表示中1的个数
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

### 补码
补码是计算机中用来表示**负数**，使得负数能够使用加法器参与加法运算的一种码。（将减法变为加法）

一个数的数值是11，他的模是16，那么他的补码是多少
16-11 = 5，即补码就是5。

模为32，使用补码运算该算式16-13，13 - 16。

16-13 = (16 + （32-13）)% 32 = 35 % 32 = 3 
13-16 = (13 + （32-16）)% 32 = 29 % 32 = 29

正数的补码即为自己
负数的补码为符号位不变，其余逐位求反再加1。

正数，符号位为0，负数，符号位为1

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>位操作</div>
现象：
我们把这个整数减1，那么原来处在整数最右边的1就会变为0
在1后面的所有的0都会变成1
其余所有位将不会受到影响。
<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@3.6/img/article/CPPoffer/weiyunsuan.jpg" width = 70% height = 35% />

1.把一个整数减去1
2.再和原整数做与运算（整数的二进制有多少个1，就可以进行多少次这样的操作）
3.直到变为0结束

</fieldset>
</form>

## 实现code
``` bash
class Solution {
public:
     int  NumberOf1(int n) {
        int count = 0;
        while(n!= 0){
            ++count;
            n = n & (n - 1);
         }
        return count;
     }
};
```