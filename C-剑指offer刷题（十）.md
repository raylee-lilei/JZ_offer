---
title: C++剑指offer刷题（十）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-22 16:20:38
tags:
keywords: 数组
description: 数组调序
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
<head>
<link rel="stylesheet" href="/css/teat.css">
</head>

## 题目描述
输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

<table><tr><td class="test">1</td><td class="test">7</td><td class="test">3</td><td class="test">2</td><td class="test">4</td><td class="test">5</td><td class="test">2</td><td class="test">3</td><td class="test">8</td><td class="test">9</td><td class="test">2</td><td class="test">7</td></tr></table><table><tr><td class="test">1</td><td class="test">7</td><td class="test">3</td><td class="test">5</td><td class="test">3</td><td class="test">9</td><td class="test">7</td><td class="test">2</td><td class="test">4</td><td class="test">2</td><td class="test">8</td><td class="test">2</td></tr></table>

<form action="" method="">
<fieldset><legend font-weight:600>思路1：</legend>
<div align=“Center”>找偶数存新数组</div>
1. 定义一个迭代器，
2. 遍历找出偶数
3. 删除偶数
4. 把偶数放回array中

<table><tr><td class="test">1</td><td class="test">7</td><td class="test">3</td><td class="test"></td><td class="test"></td><td class="test">5</td><td class="test"></td><td class="test">3</td><td class="test"></td><td class="test">9</td><td class="test"></td><td class="test">7</td></tr></table><table><tr><td class="test">2</td><td class="test">4</td><td class="test">2</td><td class="test">8</td><td class="test">2</td></tr></table><table><tr><td class="test">1</td><td class="test">7</td><td class="test">3</td><td class="test">5</td><td class="test">3</td><td class="test">9</td><td class="test">7</td><td class="test">2</td><td class="test">4</td><td class="test">2</td><td class="test">8</td><td class="test">2</td></tr></table>

</fieldset>
</form>

## 实现code1
``` bash
class Solution {
public:
    void reOrderArray(vector<int> &array) {
        vector<int> tempArray;
        vector<int>::iterator iter = array.begin();
        for(;iter!=array.end();){
            if(((*iter)&1) == 0){
                tempArray.push_back(*iter); //偶数放在临时数组中
                iter = array.erase(iter); //删除偶数的位置
            }else{
                iter++; //奇数迭代器加1
            }
        }
        //把新得的偶数放回array 中
        vector<int>::iterator iterNew = tempArray.begin();
        for(;iterNew != tempArray.end();iterNew++){
            array.push_back(*iterNew);
        }
        
    }
};
```
<form action="" method="">
<fieldset><legend font-weight:600>思路2：</legend>
<div align=“Center”>前后同时遍历</div>
1. 定义一个新数组
2. 遍历array
3. 奇数从前往后遍历 ————> 从前往后放
4. 偶数从后往前遍历 ————> 从后往前放
5. 叠加到array

first**&darr;**&emsp;&emsp;&rArr;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&lArr;&emsp;&emsp;end**&darr;**<table><tr><td class="test">1</td><td class="test">7</td><td class="test">3</td><td class="test">2</td><td class="test">4</td><td class="test">5</td><td class="test">2</td><td class="test">3</td><td class="test">8</td><td class="test">9</td><td class="test">2</td><td class="test">7</td></tr></table><table><tr><td class="test">1</td><td class="test">7</td><td class="test">3</td><td class="test">5</td><td class="test"></td><td class="test"></td><td class="test"></td><td class="test"></td><td class="test"></td><td class="test">2</td><td class="test">8</td><td class="test">2</td></tr></table>

</fieldset>
</form>


## 实现code2
``` bash
class Solution {
public:
    void reOrderArray(vector<int> &array) {
        int PreToEnd = 0;
        int EndToPre = array.size()-1;
        int *temp = new int[array.size()]();
        for (int i = 0; i < array.size(); i++) {
            if ((array[i]&1)==1) {
                temp[PreToEnd++] = array[i];
            }
            if ((array[array.size() - i - 1]&1) == 0) {
                temp[EndToPre--] = array[array.size() - i - 1];
            }
        }
        
        for(int i= 0;i<array.size();i++){
            array[i]=temp[i];
        }
       
    }
};
```


