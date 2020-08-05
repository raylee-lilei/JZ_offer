---
title: C++剑指offer刷题（五十）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-17 21:37:24
tags:
keywords: 二叉树
description: 二叉树对称
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
请实现一个函数，用来判断一颗二叉树是不是对称的。注意，如果一个二叉树同此二叉树的镜像是同样的，定义其为对称的。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>特点</div>


1. 左子树的左子树和右子树的右子树相等
2. 左子树的右子树和右子树的左子树相等

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
    //左子树的左子树和右子树的右子树相等
    //左子树的右子树和右子树的左子树相等
    bool isSymmetrical(TreeNode* pRoot)
    {
        if(pRoot == NULL){
            return true;
        }
        return IsMirror(pRoot->left,pRoot->right);
    }
    bool IsMirror(TreeNode* pRoot1,TreeNode* pRoot2){
        if(pRoot1 == NULL && pRoot2 == NULL){
            return true;
        }
        if(pRoot1 == NULL || pRoot2 == NULL){
            return false;
        }
        if(pRoot1->val != pRoot2->val){
            return false;
        }
        return(IsMirror(pRoot1->left,pRoot2->right) && IsMirror(pRoot1->right,pRoot2->left));
    }

};
```