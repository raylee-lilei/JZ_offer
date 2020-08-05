---
title: C++剑指offer刷题（四十一）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-06 11:34:34
tags:
keywords: 数组
description: 数组重复数字
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是第一个重复的数字2。
<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>hash map</div>
1. 把数组存放到hasp 表中
2. 拿出次数大于1 的数

</fieldset>
</form>

## code
``` bash 
class Solution {
public:
    // Parameters:
    //        numbers:     an array of integers
    //        length:      the length of array numbers
    //        duplication: (Output) the duplicated number in the array number
    // Return value:       true if the input is valid, and there are some duplications in the array number
    //                     otherwise false

    bool duplicate(int numbers[], int length, int* duplication) {

        if(numbers== NULL || length ==0){
            return 0;
        }
        //hash map
        int hashTable[255] = {0};
        for(int i= 0;i<length;++i){
            hashTable[numbers[i]]++;
        }
        int count = 0;
        for(int i = 0 ;i<length;++i){
            if(hashTable[numbers[i]]>1){
                duplication[count++]=numbers[i];
                return  true;
            }
        }
        return false;
    }
};
```