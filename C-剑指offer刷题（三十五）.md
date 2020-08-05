---
title: C++剑指offer刷题（三十五）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-25 12:56:40
tags:
keywords: 数组
description: 数组找出只出现一次的两个数
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。

<form action="" method="">
<fieldset><legend font-weight:600>思路1:</legend>
<div align=“Center”>异或</div>

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@5.3/img/article/CPPoffer/xor.png" width =100% height = 100% />

···异或 相同为0， 不相同为1
···a ^ a = 0
···a^0 = a
···满足结合律

1. 求出num1 ^ num2
2. 统计移位次数
3. 分组再异或找出各组的那一个值

</fieldset>
</form>

## code1 
``` bash
class Solution {
public:
    void FindNumsAppearOnce(vector<int> data,int* num1,int *num2) {
       if(data.size() == 0){
            return;
        }
        //求num1 ^ num2
        int XorResult = 0;
        for(auto x: data){
            XorResult ^= x;
        }
        
        //统计移位次数
        int SiftCount = 0;
        while((XorResult&1)==0){
            XorResult = XorResult>>1;
            ++SiftCount;
        }
        
        //分组
        for(auto x:data){
            if(((x>>SiftCount)&1) == 1){
                *num1 ^= x;
            }else{
                *num2 ^= x;
            }
        }
        return;     
    }
};
```

<form action="" method="">
<fieldset><legend font-weight:600>思路2:</legend>
<div align=“Center”>hash map </div>

1. 遍历统计出现的次数
2. 定义vector存放只出现一次的数
3. 写出求的数

</fieldset>
</form>

## code2 
``` bash
class Solution {
public:
    void FindNumsAppearOnce(vector<int> data,int* num1,int *num2) {
        //使用Map
        unordered_map<int,int> hash;
        for(auto x: data) hash[x]++;
        vector<int> temp;//存放num1 和 num2
        for(auto x:data){
           if(hash[x] ==1){
               temp.push_back(x);
           }
        }
        *num1 = temp[0];
        *num2 = temp[1];       
    }
};
```