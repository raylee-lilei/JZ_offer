---
title: C-剑指offer刷题（二十六）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-13 21:15:05
tags:
keywords: 数组
description: 数组中连续序列最大值
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
HZ偶尔会拿些专业问题来忽悠那些非计算机专业的同学。今天测试组开完会后,他又发话了:在古老的一维模式识别中,常常需要计算连续子向量的最大和,当向量全为正数的时候,问题很好解决。但是,如果向量中包含负数,是否应该包含某个负数,并期望旁边的正数会弥补它呢？
例如:{6,-3,-2,7,-15,1,2,2},连续子向量的最大和为8(从第0个开始,到第3个为止)。给一个数组，返回它的最大连续子序列的和，你会不会被他忽悠住？(子向量的长度至少是1)

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>动态规划</div>
<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@4.9/img/article/CPPoffer/shuzuzixuliehe.png" width = 100% height = 100% />
注意：
1. vector<int> F_i(array.size()) &emsp; &emsp;//分配大小
2. return *max_element(F_i.begin(),F_i.end());  &emsp; &emsp;//返回vector最大值

</fieldset>
</form>

## code
``` bash
class Solution {
public:
    int FindGreatestSumOfSubArray(vector<int> array) {
        if(array.empty()){
            return 0;
        }
        vector<int> F_i(array.size());
        F_i[0] = array[0];
        
        for(int i =1; i < array.size(); ++i){
            if(F_i[i-1]<=0){
                F_i[i] = array[i];
            }else{
                F_i[i] = F_i[i-1]+array[i];
             }
        }
        return *max_element(F_i.begin(),F_i.end()); 
        
    }
};
```