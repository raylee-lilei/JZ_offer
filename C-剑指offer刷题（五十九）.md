---
title: C++剑指offer刷题（五十九）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-30 11:42:02
tags:
keywords: 剪绳子
description: 动态规划
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
给你一根长度为n的绳子，请把绳子剪成整数长的m段（m、n都是整数，n>1并且m>1，m<=n），每段绳子的长度记为k[1],...,k[m]。请问k[1]x...xk[m]可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>动态规划 </div>


</fieldset>
</form>

## code
``` bash
class Solution {
public:
    int cutRope(int number) {
        if(number<=3){
            return number-1;
        }
        //记录最大值
        int dp[number+1];
        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 2;
        dp[3] = 3;
        int res = 0;
        for(int i =4;i<=number;++i){
            for(int j =1;j<=i/2;++j){
                res = max(res,dp[j]*dp[i-j]);
            }
            dp[i] = res;
        }
        return dp[number];
    }
};
```