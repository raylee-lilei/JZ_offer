---
title: C++剑指offer刷题（四十二）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-08 21:35:42
tags:
keywords: 数组
description: 乘积数组
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
给定一个数组A[0,1,...,n-1],请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]。不能使用除法。（注意：规定B[0] = A[1] * A[2] * ... * A[n-1]，B[n-1] = A[0] * A[1] * ... * A[n-2];）
<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>规律</div>
B[i] == A[0] A[1] A[2] A[i-1] ... A[i+1]... A[n-1]
1. 找出前半部分
2. 找出后半部分

</fieldset>
</form>

## code

``` bash 
class Solution {
public:
    vector<int> multiply(const vector<int>& A) {
        int n = A.size();
        vector<int>  B(n);
        int ret = 1;
        //B[i] == A[0] A[1] A[2] A[i-1] ... A[i+1]... A[n-1]
        //前半部分
        for(int i = 0;i< n; ret*= A[i++]){
            B[i] = ret;
        }
        ret = 1;
        //后半部分
        for(int i = n-1;i>=0;ret*= A[i--]){
            B[i] *=  ret;
        }
        return B;
    }
};
```

