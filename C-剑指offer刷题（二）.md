---
title: C++剑指offer刷题（二）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-15 08:44:11
tags:
keywords: 字符串
description: 字符串
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
<head>
<link rel="stylesheet" href="/css/teat.css">
</head>
## 题目描述
请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为I am raylee.则经过替换之后的字符串为I%20am%20raylee。
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;*originpStr **&darr;**
<table><tr><td class="test">I</td><td class="test"></td><td class="test">a</td><td class="test">m</td><td class="test"></td><td class="test">r</td><td class="test">a</td><td class="test">y</td><td class="test">l</td><td class="test">e</td><td class="test">e</td><td class="test">\0</td></tr></table>

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;*newpStr **&darr;**
<table><tr><td class="test">I</td><td class="test"></td><td class="test"></td><td class="test"></td><td class="test">a</td><td class="test">m</td><td class="test"></td><td class="test"></td><td class="test"></td><td class="test">r</td><td class="test">a</td><td class="test">y</td><td class="test">l</td><td class="test">e</td><td class="test">e</td><td class="test">\0</td></tr></table>

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>搜索从前往后搜索，插入的时候从后往前插入</div>
1.求出原始字符串大小。
2.求出空格数。
3.计算新字符串大小  blankSpaceCount*2 + originStrLen 。
4.定义两个指针指向原始和新字符串的末尾。
5.往前一次遍历：
&emsp;&emsp;当originStrLen指向空的时候，就开始替换，newpStr减一插入一个，减一插入一个，知道满足要求。
&emsp;&emsp;当originStrLen不指向空时，把原始字符串的复制给新字符串。
6.每操作完一次原始指针减一，往前遍历。
</fieldset>
</form>

## 实现code
``` bash
class Solution { 
public: 
    void replaceSpace(char *str,int length) {
        //验空
        if(str ==nullptr || length<=0 ){
            return;
        }
        //求出原始字符串长度
        int blankSpaceCount = 0;
        int originStrLen = 0;
        //求出空格数
       for(int i = 0;str[i]!='\0';i++){
           originStrLen++;
           if(str[i]==' '){
               blankSpaceCount++;
           }
       }
        int newStrLen = blankSpaceCount*2 + originStrLen;
        char *originpStr = str + originStrLen;
        char *newpStr = str + newStrLen;
        while(originpStr < newpStr){
            if(*originpStr== ' '){
                *newpStr-- = '0';
                *newpStr-- = '2';
                *newpStr-- = '%';
            }else{
                *newpStr--= *originpStr;
            }
            originpStr--;
        }
}
};
```

