---
title: C++剑指offer刷题（五十三）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-20 12:58:25
tags:
keywords: 二叉搜索树
description: 二叉搜索树中序遍历
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
给定一棵二叉搜索树，请找出其中的第k小的结点。例如， （5，3，7，2，4，6，8）    中，按结点数值大小顺序第三小结点的值为4。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>中序遍历的结果按照从小到大的顺序排列的</div>


1. 遍历左子树
2. k--
3. 如果k==0，res = 节点
4. 遍历右子树

</fieldset>
</form>

## code
``` bash
/*
struct TreeNode {
    int val;
    struct TreeNode *left;
    struct TreeNode *right;
    TreeNode(int x) :
            val(x), left(NULL), right(NULL) {
    }
};
*/
class Solution {
public:
    TreeNode* res = NULL;
    //中序遍历结果就是从小到大顺序
    TreeNode* KthNode(TreeNode* pRoot, int k)
    {
        DFS(pRoot,k);
        return res;
    }
    void DFS(TreeNode* pRoot, int &k){
        if(!pRoot){
            return;
        }
        //左
        DFS(pRoot->left,k);
        //根
        k--;
        if(k==0){
            res = pRoot;
        }
        //右
        DFS(pRoot->right,k);
    }

    
};
```