---
title: C++剑指offer刷题（七）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-19 11:51:20
tags:
keywords: 斐波那契数列
description: 输出斐波那契数列某个数
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

<head>
<link rel="stylesheet" href="/css/teat.css">
</head>
## 题目描述
要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0）。
n:<table><tr><td class="test">0</td><td class="test">1</td><td class="test">2</td><td class="test">3</td><td class="test">4</td><td class="test">5</td><td class="test">6</td><td class="test">7</td><td class="test">8</td><td class="test">9</td></tr></table>斐波那契数列:<table><tr><td class="test">0</td><td class="test">1</td><td class="test">1</td><td class="test">2</td><td class="test">3</td><td class="test">5</td><td class="test">8</td><td class="test">13</td><td class="test">21</td><td class="test">34</td></tr></table>

<form action="" method="">
<fieldset><legend font-weight:600>思路1：</legend>
<div align=“Center”>动态数组记录前两项的值，当前项只需要进行一次加法运算</div>
1.申请一个动态数组存放前两项的值，要输出某一项只需要将前两项相加
2.输出数组中的某项
3.释放空间

这样时间复杂度O(n)，空间复杂度O(n)
</fieldset>
</form>

## 实现code1
``` bash
class Solution {
public:
    int Fibonacci(int n) {
        int temp;
        if(n<=0)
            return 0;
        int *Arraylist=new int[n+1];
        Arraylist[1]=Arraylist[2]=1;
        for(int i=3;i<=n;i++)
        {
            Arraylist[i]=Arraylist[i-1]+Arraylist[i-2];
        }
        
        temp=Arraylist[n];
        return temp;
        delete []Arraylist;
    
 }
};
```

<form action="" method="">
<fieldset><legend font-weight:600>思路2：</legend>
<div align=“Center”>迭代法</div>
中间的结果不需要记录

1.每次记录前一项
2.迭代辗转相加

这样时间复杂度O(n)，空间复杂度O(1)
</fieldset>
</form>

## 实现code2

``` bash
class Solution {
public:
    int Fibonacci(int n) {
        int i;
        int PreItem =0;
        int CurrentItem =1;
        if(n<=0)
            return 0;
        if(n==1)
            return 1;
        for(i=2;i<=n;i++){
            CurrentItem = PreItem+CurrentItem;
            PreItem = CurrentItem-PreItem;
        }
        return CurrentItem;
 }
};
```

## 斐波那契数列的应用

### 跳台阶
一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。

<form action="" method="">
<fieldset><legend font-weight:600>思路1：</legend>
<div align=“Center”>数组保存记录前面的值</div>

对于第n个台阶来说，只能从n-1或者n-2的台阶跳上来，所以
F(n) = F(n-1) + F(n-2)
斐波拉契数序列，初始条件
n=1:只能一种方法
n=2:两种
刚好满足斐波拉契数列
</fieldset>
</form>


### 实现code1
``` bash
class Solution {
public:
    int jumpFloor(int number) {
        int temp;
        int *Arraylist=new int[number+1];
        Arraylist[0]=1;
        Arraylist[1]=1;
        for(int i=2;i<=number;i++)
        {
            Arraylist[i]=Arraylist[i-1]+Arraylist[i-2];
        }       
        temp=Arraylist[number];
        return temp;
        delete []Arraylist;
    }
};
```

<form action="" method="">
<fieldset><legend font-weight:600>思路2：</legend>
<div align=“Center”>迭代法</div>
中间的结果不需要记录

1.每次记录前一项
2.迭代辗转相加

</fieldset>
</form>

### 实现code2
``` bash
class Solution {
public:
    int jumpFloor(int number) {
        int i;
        int PreItem =1;
        int CurrentItem =1;
        if(number<=0)
            return 0;
        if(number==1)
            return 1;
        for(i=2;i<=number;i++){
            CurrentItem = PreItem+CurrentItem;
            PreItem = CurrentItem-PreItem;
        }
        return CurrentItem;
    }
};

```

### 变态跳台阶
一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>位操作</div>

n = 1 1中跳法
n = 2 2中跳法
n = 3 4中跳法
n = 4 8中跳法
...
n = number  2 ^(number - 1)  中跳法

直接按位操作
m*2^n  相当于将m左移n次
m/2^n  相当于将m右移n次
</fieldset>
</form>

### 实现code

``` bash 
class Solution {
public:
    int jumpFloorII(int number) {
        int  shift = 1;  //将要移位的数  1* 2^(n-1)
        return 1<<(number - 1);
    }
};
``` 

### 矩形覆盖
我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？
<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@3.5/img/article/CPPoffer/juxing.png" width = 60% height = 40% />

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>迭代法</div>

  其实也是斐波拉契数列

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@3.5/img/article/CPPoffer/juxingfenxi.jpg" width = 70% height = 25% />

</fieldset>
</form>

### 实现code
``` bash
class Solution {
public:
    int rectCover(int number) {
        int i;
        int PreItem =1;
        int CurrentItem =1;
        if(number<=0)
            return 0;
        if(number==1)
            return 1;
        for(i=2;i<=number;i++){
            CurrentItem = PreItem+CurrentItem;
            PreItem = CurrentItem-PreItem;
        }
        return CurrentItem;
    }
};
```