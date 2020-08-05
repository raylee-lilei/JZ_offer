---
title: C++剑指offer刷题（三十三）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-23 13:13:14
tags:
keywords: 数组
description: 统计数字次数
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
统计一个数字在排序数组中出现的次数。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>二分法</div>

1. 将数组二分
2. 二分直到 找到和k 相同的位置
3. 相同位置 往前找相同数
4. 相同位置 往后找相同数
5. 返回计数

</fieldset>
</form>

## code
``` bash 
class Solution {
public:
    int GetNumberOfK(vector<int> data ,int k) {
        //二分法找中间
        int Len = data.size();
        if(Len ==0){
            return 0;
        }
        int start = 0,mid = 0,end = Len-1,count=0;
        //二分直到 找到和k 相同的位置
        while(start < end){
            mid = (end + start)>>1;
            if(k<data[mid]){
                end = mid-1;
            }
            if(k>data[mid]){
                start = mid+1;
            }
            if(k == data[mid]){
                break;
            }
        }
        //相同位置 往前找相同数
        int i = mid;
        while(i>=0 && k==data[i]){
            --i;
            ++count;
        }
        //相同位置 往后找相同数
        i = mid+1;
        while(i<Len && k==data[i]){
            ++i;
            ++count;
        }
        
        return count;
    }
};
```