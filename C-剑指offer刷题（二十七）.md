---
title: C-剑指offer刷题（二十七）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-15 09:40:50
tags:
keywords: 数字规律
description: 数字中有1的个数
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
求出1~13的整数中1出现的次数,并算出100~1300的整数中1出现的次数？为此他特别数了一下1~13中包含1的数字有1、10、11、12、13因此共出现6次,但是对于后面问题他就没辙了。ACMer希望你们帮帮他,并把问题更加普遍化,可以很快的求出任意非负整数区间中1出现的次数（从1 到 n 中1出现的次数）。


<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>规律</div>
<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@5.0/img/article/CPPoffer/1degeshu.png" width = 80% height = 80% />

1. 找出当前位、高位、低位
2. 判断当前位是0、1、大于1
3. 遍历个十百千位...
</fieldset>
</form>

## code 

``` bash
class Solution {
public:
    int NumberOf1Between1AndN_Solution(int n)
    {
        if( n<=0 ){
            return 0;
        }
       
        int count = 0;
        int digit = 1;   //个十百千..1.10  100  1000
        
        while(n/digit!=0){
        int CurNum = (n/digit)%10;  //数字的当前个十百千位
        int HightNum = n/(digit*10); //当前位前面的数字
        int LowNum = n % digit;   //当前位后面的数字
            
        if(CurNum == 0){
            count += HightNum * digit;
        }else if(CurNum == 1){
            count += HightNum*digit + LowNum +1;
        }else{
            count += digit*(HightNum +1);
             }
            digit *= 10;
        }
        
        return count;
    }
};
```