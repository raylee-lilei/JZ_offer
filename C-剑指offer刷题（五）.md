---
title: C++剑指offer刷题（五）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-18 13:21:06
tags:
keywords: 队列、栈
description: 两个栈表示一个队列
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>一个栈存放入队列，另一个栈用来出队列</div>
1.对列入队：借助stack1的压栈push
2.对列出对：
&emsp;&emsp;&emsp; ●借助stack2，把stack1出栈的值放入stack2中
&emsp;&emsp;&emsp; ●stack2出栈也就是队列的出对
</fieldset>
</form>

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@3.4/img/article/CPPoffer/stackfenxi.jpg" width = 70% height = 30% />

## 实现code
``` bash
class Solution
{
public:
    void push(int node) {
        stack1.push(node);
    }

    int pop() {
       if(stack2.empty()){
           while(!stack1.empty()){
               stack2.push(stack1.top());
               stack1.pop();
           }
       }
       int QueenTemp = stack2.top();
       stack2.pop();
       return QueenTemp;
    }

private:
    stack<int> stack1;
    stack<int> stack2;
};
```