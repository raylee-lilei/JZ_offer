---
title: C++剑指offer刷题（三十七）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-27 21:12:36
tags:
keywords: 字符串
description: 左移字符串
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
汇编语言中有一种移位指令叫做循环左移（ROL），现在有个简单的任务，就是用字符串模拟这个指令的运算结果。对于一个给定的字符序列S，请你把其循环左移K位后的序列输出。例如，字符序列S=”abcXYZdef”,要求输出循环左移3位后的结果，即“XYZdefabc”。是不是很简单？OK，搞定它！

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>截取字符串</div>

1. 拿出前n位
2. 删除前n位
3. 拿出的前n位放到str之后 

</fieldset>
</form>

## code
```bash
class Solution {
public:
    string LeftRotateString(string str, int n) {
        
        /*
        //截取前n位插入字符串的后面
        string tempStr="";
        if(n<0){
            return NULL;
        }
        if(n==0){
            return str;
        }
        tempStr = str.substr(0,n); //从第0 位开始截取str的n-1 个数
        str.erase(0,n);
        str+=tempStr;
        return str;
        
        */
        if(n<0){
            return NULL;
        }
        if(n==0){
            return str;
        }
        string tempStr = "";
        for(int i = n;i<str.size();++i){
            tempStr.push_back(str[i]);
        }
        for(int i = 0;i<n;++i){
            tempStr.push_back(str[i]);
        }
        return tempStr;
    }
};
```