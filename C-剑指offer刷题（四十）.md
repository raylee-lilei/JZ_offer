---
title: C++剑指offer刷题（四十）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-05 16:54:35
tags:
keywords: 数学公式 
description: 条件限制
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
每年六一儿童节,牛客都会准备一些小礼物去看望孤儿院的小朋友,今年亦是如此。HF作为牛客的资深元老,自然也准备了一些小游戏。其中,有个游戏是这样的:首先,让小朋友们围成一个大圈。然后,他随机指定一个数m,让编号为0的小朋友开始报数。每次喊到m-1的那个小朋友要出列唱首歌,然后可以在礼品箱中任意的挑选礼物,并且不再回到圈中,从他的下一个小朋友开始,继续0...m-1报数....这样下去....直到剩下最后一个小朋友,可以不用表演,并且拿到牛客名贵的“名侦探柯南”典藏版(名额有限哦!!^_^)。请你试着想下,哪个小朋友会得到这份礼品呢？(注：小朋友的编号是从0到n-1)

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>约瑟夫环</div>

直接return （（递归 删除一个小朋友） +m）%n

</fieldset>
</form>

## code1
``` bash 
class Solution {
public:
    int LastRemaining_Solution(int n, int m)
    {
        if(n<=0){
            return -1;
        }
        return (LastRemaining_Solution(n-1,m)+m)%n;
    }
};
```

## 题目描述2
求1+2+3+...+n，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。
<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>判断条件转化&</div>

</fieldset>
</form>

## code2
``` bash 
class Solution {
public:
    int Sum_Solution(int n) {
        int result = n;
        (n>0) && (result += Sum_Solution(n-1));
        return result;
    }
};
```

## 题目描述3
写一个函数，求两个整数之和，要求在函数体内不得使用+、-、*、/四则运算符号。
<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>异或^</div>
1. 两个数取异或（相同为0，不相同为1）特性就是不进位的加法
2. 两个数取&左移1位确定进位数
3. num1 = num1^num2
4. num2 = (num1&num2)<<1;
5. 进位为0结束
</fieldset>
</form>

## code3
``` bash 
class Solution {
public:
    int Add(int num1, int num2)
    {
        int sum,carryLShift;
        while(num2!=0){
            sum = num1^num2;
            carryLShift = (num1&num2)<<1;
            num1 = sum;
            num2 = carryLShift;
        }
        return num1;
    }
};
```