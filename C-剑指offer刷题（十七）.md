---
title: C++剑指offer刷题（十七）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-29 12:32:33
tags:
keywords: 栈
description: 栈弹出
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。
例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。
（注意：这两个序列的长度是相等的）

>由于栈的压入过程中可以向外弹元素，不一定是全部元素进栈才开始向外弹栈，所以会产生不同的弹栈顺序。
>压入 1、2、3、4时 &emsp;&emsp;&emsp;&emsp;弹出4
>压入5 &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;弹出5
> &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; 弹出3、2、1
>所以弹出4,5,3,2,1

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>借助一个辅助vector</div>
1. 遍历序列1，依次存入辅助vector  TempArray中
2. 遍历的同时比较依次插入TempArray中的最后一个元素是否和序列2 中的第一个元素相等
3. 如果不相等继续往下遍历序列1
4. 如果相等，就把TempArray的最后一个元素删除，再比较序列2中的下一个元素
5. 最后返回TempArray是否为空，为空则是弹出序列

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@4.4/img/article/CPPoffer/zhantanchu.png" width = 90% height = 80% />

</fieldset>
</form>

## code
``` bash
class Solution {
public:
    bool IsPopOrder(vector<int> pushV,vector<int> popV) {
        if(pushV.empty()){
            return false;
        }
        vector<int> TempArray;
        for(int i=0,j =0;i<=pushV.size()-1;i++){
            TempArray.push_back(pushV[i]);
            while(j<=pushV.size()-1 && TempArray.back() == popV[j]){
                TempArray.pop_back();
                j++;
            }
        }
        return TempArray.empty();
    }
};
```