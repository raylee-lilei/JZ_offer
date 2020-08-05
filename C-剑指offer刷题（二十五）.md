---
title: C-剑指offer刷题（二十五）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-12 20:10:59
tags:
keywords: 数组
description: 数组中最小的k个值
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 输入n个整数，找出其中最小的K个数。
例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>sort排序</div>
1. sort排序
2. 前k个就是最小
</fieldset>
</form>

## code
``` bash 
class Solution {
public:
    vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {
        vector<int> MinResult;
        int size = input.size();
        if(input.empty()||k>size){
            return MinResult;
        }
        sort(input.begin(),input.end());
        
        for(int i = 0;i<k;++i){
            MinResult.push_back(input[i]);
        }
        return MinResult;
    }
};
```