---
title: C++剑指offer刷题（五十六）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-30 11:39:55
tags:
keywords: 滑动窗口
description: 数组
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
给定一个数组和滑动窗口的大小，找出所有滑动窗口里数值的最大值。例如，如果输入数组{2,3,4,2,6,2,5,1}及滑动窗口的大小3，那么一共存在6个滑动窗口，他们的最大值分别为{4,4,6,6,6,5}； 针对数组{2,3,4,2,6,2,5,1}的滑动窗口有以下6个： {[2,3,4],2,6,2,5,1}， {2,[3,4,2],6,2,5,1}， {2,3,[4,2,6],2,5,1}， {2,3,4,[2,6,2],5,1}， {2,3,4,2,[6,2,5],1}， {2,3,4,2,6,[2,5,1]}。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>队列</div>

1. 定义一个队列，存放数组的下标
2. 当后一个比 队列中下标的值大，删除队列中的元素（最大的排在最前面）
3. 队列中插入下标
4. 如果窗口都划出了size个了，某个值还是最大，删除前面的大值
5. 只要大于3之后每次都将队列最前面的值插入结果中

</fieldset>
</form>

## code
``` bash
class Solution {
public:
    vector<int> maxInWindows(const vector<int>& num, unsigned int size)
    {
         vector<int> result;
        if(size<1 || num.size()<size){
            return result;
        }
        deque<int> qmax;
        for(int i=0; i<num.size(); ++i){
            //遍历大小，最大的排在最前面
            while(!qmax.empty() && num[qmax.back()]<=num[i]){
                qmax.pop_back();
            }
            //队列插入下标
            qmax.push_back(i);
            
            //如果窗口都划出了size个了，某个值还是最大，删除前面的大值
            if(qmax.front() == i-size)
                {
                qmax.pop_front();
            }
            //只要大于3之后每次都将最前面的值插入结果中
            if(i >= size - 1){
                result.push_back(num[qmax.front()]);
            }
        }
        return result; 
    }
};
```