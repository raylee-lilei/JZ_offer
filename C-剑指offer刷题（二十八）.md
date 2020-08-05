---
title: C-剑指offer刷题（二十八）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-18 14:11:03
tags:
keywords: 数组
description: 数组拼接排序
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。
例如输入数组{3，32，321}，则打印出这三个数字能排成的最小数字为321323。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>数组转字符串</div>

1. a + b < b + a 则  a  排在前面
2. 利用sort排序，排序方式按照camp 排序
2. 输出字符串

</fieldset>
</form>


## code

``` bash 
class Solution {
public:
    static bool camp(int a, int b){
        string a_s = to_string(a);
        string b_s = to_string(b);
        return a_s + b_s < b_s + a_s;
    }
    string PrintMinNumber(vector<int> numbers) {
        string result;
        sort(numbers.begin(),numbers.end(),camp);
        for(auto x :numbers){
            result += to_string(x);
        }
        return result;
    }
};

```