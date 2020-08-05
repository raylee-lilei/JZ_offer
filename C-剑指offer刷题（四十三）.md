---
title: C++剑指offer刷题（四十三）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-08 21:38:00
tags:
keywords: 正则表达式
description: 匹配正则表达式
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
请实现一个函数用来匹配包括'.'和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（包含0次）。 在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但是与"aa.a"和"ab*a"均不匹配
<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>递归</div>
B[i] == A[0] A[1] A[2] A[i-1] ... A[i+1]... A[n-1]
1. str 和pattern都为空 
2. str不为空 pattern为空
3. 都不为空
&emsp;&emsp;&emsp;(1).（aaa&emsp;&emsp;a.a;aaa&emsp;&emsp;.aa ）pattern+1不是为*，第一个相同继续比较下一个；str不为空，pattern为.继续比较下一个
&emsp;&emsp;&emsp;(2).（aa&emsp;&emsp;a*aa;aaa&emsp;&emsp;.*a ）pattern+1为*,第一个相同继续比较下一个pattern跳过两个；str不为空，pattern为.str向下移动;否则（aa&emsp;&emsp;c*aa）pattern跳过两个
</fieldset>
</form>

## code

``` bash 
class Solution {
public:
    bool match(char* str, char* pattern)
    {
        if(*str =='\0' && *pattern == '\0'){
            return true;
        }
        if(*str !='\0' && *pattern == '\0'){
            return false;
        }
        
        //都不为空
        if(*(pattern+1) != '*'){ //aaa  a.a    aaa   .aa
            if(*str == *pattern || (*str != '\0')&& *pattern == '.'){
                return match(str+1,pattern+1);
            }else{
                return false;
            }
        }else{
            if(*str == *pattern || (*str != '\0')&& *pattern == '.'){
                return match(str,pattern+2) || match(str+1,pattern);
                //aa a*aa
                //aaa .*a 只需要看str 是否相同，.* *可以为n个
            }else{ // aa    c*aa
                return match(str,pattern+2);
            }
        }
    }
};
```