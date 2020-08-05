---
title: C++剑指offer刷题（十六）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-28 11:23:33
tags:
keywords: 栈
description: 栈操作找Min
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---


## 题目描述
定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。
注意：保证测试中不会当栈为空的时候，对栈调用pop()或者min()或者top()方法。

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>借助一个辅助栈找min</div>
1. 对操作栈压栈，辅助栈压入一个值
2. 比较压入栈的值与栈顶元素的大小；如果小就压栈，否则不压栈
3. 如果辅助栈的值与操作栈的值相等辅助栈出栈
4. 操作栈出栈
5. 返回操作栈栈顶元素
6. 返回辅助栈栈顶元素就是最小值

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@4.3/img/article/CPPoffer/stackMin.png" width = 100% height = 100% />

</fieldset>
</form>


## code
``` bash 
class Solution {
public:
    stack<int> StackStructure,AssistStack; 
    void push(int value) {
        StackStructure.push(value);
        if(AssistStack.empty()){
            AssistStack.push(value);
        }else if(value <= AssistStack.top()){
            AssistStack.push(value);
          }
    }
    void pop() {
        if(StackStructure.top() == AssistStack.top()){
            AssistStack.pop();
        }
        StackStructure.pop();
    }
    int top() {
        return StackStructure.top();
    }
    int min() {
        return AssistStack.top();
    }
};
```