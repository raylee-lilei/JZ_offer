---
title: C++剑指offer刷题（三十）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-21 09:28:09
tags:
keywords: 字符串
description: 字符串中出现一次的数字
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
在一个字符串(0<=字符串长度<=10000，全部由字母组成)中找到第一个只出现一次的字符,并返回它的位置, 如果没有则返回 -1（需要区分大小写）.（从0开始计数）

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>hash map</div>

1. 定义一个hash表 unordered_map<char,int> hash
2. 遍历统计每个字符出现的次数
3. 遍历出满足出现的次数

</fieldset>
</form>


## code

``` bash
class Solution {
public:
    int FirstNotRepeatingChar(string str) {
        if(str.size() == 0) return -1;
        //遍历统计每个字符出现的次数
        unordered_map<char,int> hash;
        for(auto x : str){
            ++hash[x];
        }
        //遍历出现的次数
        for(int i = 0;i<str.length();++i){
            if(hash[str[i]] == 1){
                return i;
            }
        }
        return  -1;
    }
};
```