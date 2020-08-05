---
title: C-剑指offer刷题（二十三）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-08 10:06:35
tags:
keywords: 字符串排序
description: 字符串全排列输出字典序列
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

##题目描述
输入一个字符串,按字典序打印出该字符串中字符的所有排列。
例如输入字符串abc,则打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>递归</div>

1. 全排列
&emsp;&emsp;（1）检查输出的字符串长度是否等于输入长度
&emsp;&emsp;（2）如果相等使用find 函数判断是否存在重复的，添加不重复的

&emsp;&emsp;&emsp;&emsp;find(result.begin(),result.end(),str) == result.end() 
&emsp;&emsp;&emsp;&emsp;&emsp;返回的是指针
&emsp;&emsp;&emsp;&emsp;&emsp;如果在查找范围内不存在，返回result.end()
&emsp;&emsp;（3）固定位置，字符依次同后面字符交换
&emsp;&emsp;（4）递归后面字符的排列
&emsp;&emsp;（5）还原交换前的状态

2. 结果按字典排序

</fieldset>
</form>

## code
``` bash
class Solution {
public:
    //(1) 遍历出所有可能出现在第一个位置的字符
    //(2) 固定第一个字符，求后面字符的排列
    vector<string> Permutation(string str) {
        vector<string> result;
        if(str.empty()){
            return result;
        }
        //全排列
        Permutation(str,result,0);
        //结果按字典排序
        sort(result.begin(),result.end());
        return result;
    }
    
    void Permutation(string str,vector<string> &result,int state){
        //结束条件，输出的字符串长度==输入的字符串长度
        if(state == str.size()-1){
            //find  返回的是指针
            // 如果在查找范围内不存在，返回a.end()
            
            //如果result中不存在str，才添加；避免重复添加的情况
            if(find(result.begin(),result.end(),str) == result.end()){
                result.push_back(str);
            }
        }else{
            for(int i= state;i<str.size();i++){
                //state 用来固定位置,第一个字符同后面所有字符交换
                swap(str[i],str[state]);
                //后面字符的排列——递归
                Permutation(str,result,state+1);
                //还原交换前的状态
                swap(str[i],str[state]);
            }
        }
    }
    
    void swap(char &str1 ,char &str2){
        char temp ;
        temp = str1;
        str1 = str2;
        str2 = temp;
    }
    
};
```