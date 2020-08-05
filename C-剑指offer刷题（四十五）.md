---
title: C++剑指offer刷题（四十五）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-14 13:12:11
tags:
keywords: 字符串
description: hash表
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符"go"时，第一个只出现一次的字符是"g"。当从该字符流中读出前六个字符“google"时，第一个只出现一次的字符是"l"。
如果当前字符流没有存在出现一次的字符，返回#字符。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>hash map</div>

1. 输入字符串存入vec 中，然后写出hash表
2. 遍历hash表，返回表中的值为1的数

</fieldset>
</form>

## code

``` bash
class Solution
{
public:
  //Insert one char from stringstream
    string vec;
    char hash[255] = {0};
    void Insert(char ch)
    {
        vec += ch;
        hash[ch]++;
    }
  //return the first appearence once char in current stringstream
    char FirstAppearingOnce()
    {
        for(int i =0;i<vec.size();++i){
            if(hash[vec[i]]==1){
                return vec[i];
            }
        }
        return '#';
    }

};
```