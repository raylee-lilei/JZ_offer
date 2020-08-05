---
title: C++剑指offer刷题（三十八）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-28 22:07:39
tags:
keywords: 字符串
description: 字符串单词排序
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
牛客最近来了一个新员工Fish，每天早晨总是会拿着一本英文杂志，写些句子在本子上。同事Cat对Fish写的内容颇感兴趣，有一天他向Fish借来翻看，但却读不懂它的意思。例如，“student. a am I”。后来才意识到，这家伙原来把句子单词的顺序翻转了，正确的句子应该是“I am a student.”。Cat对一一的翻转这些单词顺序可不在行，你能帮助他么？

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>字符串拼接</div>
<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@5.4/img/article/CPPoffer/zimupaixu.png" width =100% height = 100% />

1. 定义一个临时数组存放一个单词
2. 遇到空格就把该单词存放在result中（注意拼接顺序）
3. 确定最后一个单词，拼接在result中

</fieldset>
</form>

## code
``` bash 
class Solution {
public:
    string ReverseSentence(string str) {
        string result = "";
        string tempArray = "";
        for(int i = 0;i<str.size();++i){
            if(str[i]== ' ' ){
                result = " " + tempArray + result;
                tempArray = "";
            }else{
                tempArray+=str[i];
            }
        }
        if(tempArray.size()){
            result = tempArray + result;
        }
        return result;
    }
};
```