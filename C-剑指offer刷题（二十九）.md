---
title: C-剑指offer刷题（二十九）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-20 20:02:21
tags:
keywords: 丑数
description: 丑数数组
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
把只包含质因子2、3和5的数称作丑数（Ugly Number）。
例如6、8都是丑数，但14不是，因为它包含质因子7。 习惯上我们把1当做是第一个丑数。求按从小到大的顺序的第N个丑数。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”></div>

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@5.1/img/article/CPPoffer/choushu.png" width = 100% height = 100% />

1. 定义一个丑数数组
2. 定义三个数分别指向乘以2、3、5的虚队列
3. 找到分别乘以2,3,5的虚拟队列的最小值
4. 如果最小值与乘以2,3,5中P指向相等，则把P指向的数插入到丑数数组中，并且指向往后移
5. 返回丑数数组最后一个数

</fieldset>
</form>

## code
``` bash
class Solution {
public:
    int GetUglyNumber_Solution(int index) {
        if (index <= 0){
            return 0;
        }
        if(index < 7){
            return index;
        }
        vector<int> UglyResult;
        int P2= 0,P3 =  0,P5 = 0; 
        int MinUgly = 1;
        UglyResult.push_back(MinUgly);
        while(UglyResult.size() < index){
            MinUgly = min(UglyResult[P2]*2,min(UglyResult[P3]*3,UglyResult[P5]*5));
            if(UglyResult[P2]*2 == MinUgly) ++P2;
            if(UglyResult[P3]*3 == MinUgly) ++P3;
            if(UglyResult[P5]*5 == MinUgly) ++P5;
             UglyResult.push_back(MinUgly);
        }
        return UglyResult.back();
    }
};
```
