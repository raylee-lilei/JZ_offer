---
title: C++剑指offer刷题（九）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-21 16:12:03
tags:
keywords: 指数
description: 指数计算
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。保证base和exponent不同时为0。
*********************
n为奇数时, n&1为1
n为偶数时, n&1为0
n&1等效于  n%2==1

"n>> 1"与操作与"n/2"

1. . >>是右移符号，它在操作时只允copy许整数
   . /是除法，它可以操作不同类型的数据(int  float)
2. 右移操作通常情况下，会比整数除法速度快
3. 右移运算的优先级比除法低，先计算乘除，后计算左移或右移


<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>指数计算</div>

1. 先判断base==0  exponent > 0   结果为0       否则错误
2. 判断base！=0   exponent > 0   计算公式计算   exponent = 0  计算结果为1     exponent < 0   去倒数
3. 计算公式 
<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@3.7/img/article/CPPoffer/zhishujisuan.png" width = 70% height = 35% />
</fieldset>
</form>

## 实现code

``` bash
class Solution {
public:
    double Power(double base, int exponent) {
        if(base == 0){
            if(exponent >0){return 0;}
            else {
                throw std::invalid_argument("input error（divisor！=0）||0 at the same time）");
            }
         }else{
            if(exponent > 0){ return PerformOperation(base,exponent);}
            else if(exponent == 0){return 1;}
            else{return 1/PerformOperation(base,-exponent);}
             }
    }
    
    double PerformOperation(double base,int exponent){
        if(exponent == 1){return base;}
        if((exponent & 1) ==0){
            double Temp_Even = PerformOperation(base,exponent >> 1);
            return Temp_Even*Temp_Even;
        }else{
            double Temp_Odd = PerformOperation(base,(exponent - 1) >> 1);
            return Temp_Odd*Temp_Odd*base;
        }
    }
};
```