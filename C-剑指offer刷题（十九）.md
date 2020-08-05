---
title: C++剑指offer刷题（十九）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-01 21:28:12
tags:
keywords: 二叉搜索树
description: 后序遍历二叉搜索树
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
输入一个非空整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出Yes,否则输出No。假设输入的数组的任意两个数字都互不相同。

### 二叉搜索树
二叉搜索树左子树值都比根小，右子树值都比根大。

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@4.5/img/article/CPPoffer/erchasosuoshu.png" width = 70% height = 70% />

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>后序遍历二叉搜索树</div>
1. 后序遍历的最后一个元素为根
2. 定义两个vector存放前部分左子树，后半部分右子树
3. 找出分界线 i
4. 前部分放入leftArray；后半部分放入rightArray
5. 递归继续1——4步骤，判断左右子树
6. 左右子树都是如此划分的就放回true
</fieldset>
</form>

## code 
``` bash
class Solution {
public:
    bool VerifySquenceOfBST(vector<int> sequence) {
        //存放数组前半部分左子树， 后半部分右子树
        vector<int> leftArray,rightArray;
        int  TreeRoot = sequence.back();
        if(sequence.empty()){
            return false;
        }
        //找出分解线
        int i = 0;//把i写成去全局
        for(;i < sequence.size()-1;++i){
            if(sequence[i]>TreeRoot)
                break;
        }
        //判断右边
        for(int j = i;j<sequence.size()-1;++j){
            if(sequence[j]<TreeRoot)
               return false;
            }
        //前半部分放入左子树
        for(int m = 0;m < i;++m){
            leftArray.push_back(sequence[m]);
        }
        //后半部分放入右子树
        for(int n = i;n < sequence.size()-1;++n){
            rightArray.push_back(sequence[n]);
        }
        //判断左右子树是否为二叉搜索树
        bool leftTree = true;
        bool rightTree = true;
        if(leftArray.size()>0){
            leftTree = VerifySquenceOfBST(leftArray);
        }
        if(rightArray.size()>0){
            rightTree = VerifySquenceOfBST(rightArray);
        }
        return (leftTree && leftTree);
    }
};

```