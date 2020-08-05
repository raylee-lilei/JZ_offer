---
title: C++剑指offer刷题（四十四）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-08 21:38:25
tags:
keywords: 字符串
description: 字符串数字
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100","5e2","-123","3.1416"和"-1E-16"都表示数值。 但是"12e","1a3.14","1.2.3","+-5"和"12e+4.3"都不是。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>特点</div>

1. +-15
2. +  || -
3. 两个 . . false
4. e10(e前面没有数)   1e12e（e前面已经有一个e）
5. e +
6. e + -
7. e后面没有数

</fieldset>
</form>

## code

``` bash 
class Solution {
public:
    bool isNumeric(char* string)
    {
        //e 后面没有数字
        //有其他字符
        //两个小数点
        //+-连续
        //e后面有小数点
        if(string == NULL){
            return false;
        }
        
        if(*string == '+' || *string == '-'){
            string++;
            //+- 15
            if(*string == '+' || *string == '-'){
                return false;
            }
            //+  || -
            if(*string = '\0'){
            return false;
            }
        }
        int decimal = 0,e = 0,number = 0;
        while(*string != '\0'){
            if(*string >= '0' && *string<= '9'){
                string++;
                number++;
            }else if(*string == '.'){
                // 两个小数点 ..  不行
                //e后面有.不行
                if(decimal>0 || e >0){
                    return false;
                }
                string++;
                decimal++;   
            }else if(*string == 'e' || *string == 'E'){
                //e10(e前面没有数)   1e12e（e前面已经有一个e）
                if(number == 0 || e> 0){
                    return  false;
                }
                string++;
                e++;
                //e+
                if(*string == '+' || *string == '-'){
                    string++;
                    //e+ +
                    if(*string == '+' || *string == '-'){
                        return false;
                    }
                }
                //e后面没有数
                if(*string == '\0'){
                    return false;
                }
            }else{
                return false;
            }
        }
        return true;
        
    }

};
```
