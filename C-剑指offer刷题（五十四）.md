---
title: C++剑指offer刷题（五十四）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-30 11:39:17
tags:
keywords: 字符串
description: 字符串转化为整数
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
将一个字符串转换成一个整数，要求不能使用字符串转换整数的库函数。 数值为0或者字符串不是一个合法的数值则返回0

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>遍历</div>

1. 定义 一个标记位
2. 判断第一个为‘-’，标记位为 -1，否则为1
3. 开始遍历，若果第一个字符为‘-’，就从第二个位置开始
4. 判断后面的字符是否是数字
5. 转化为数字
6. 乘以标记位得到结果

</fieldset>
</form>

## code
``` bash
class Solution {
public:
    int StrToInt(string str) {
        int len=str.length();
        int result;
        if(len<0) result=0;
        int flag;
        if(str[0]=='-')
            flag=-1;
        else flag=1;

        for(int i=(str[i]=='-'||str[i]=='+')?1:0;i<len;++i)
            {
            if(!(str[i]>='0'&&str[i]<='9'))//不在范围内的返回0
                {
                return 0;
            }
           result=result*10+str[i]-'0';//范围内的字符转换为整数
        }
        return result*flag;

    }
};
```