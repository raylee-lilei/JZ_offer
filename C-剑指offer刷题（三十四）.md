---
title: C++剑指offer刷题（三十四）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-24 14:05:50
tags:
keywords: 二叉树、平衡二叉树
description: 二叉树深度
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述1
输入一棵二叉树，求该树的深度。从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>递归</div>

1. 递归遍历左子树
2. 递归遍历右子树
3. 返回最大值加一

</fieldset>
</form>

## code1
``` bash
/*
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};*/
class Solution {
public:
    int TreeDepth(TreeNode* pRoot)
    {
        if(pRoot ==  NULL) return 0;
        return max(TreeDepth(pRoot->left),TreeDepth(pRoot->right))+1;
    }
};
```

## 题目描述2
输入一棵二叉树，判断该二叉树是否是平衡二叉树。
在这里，我们只需要考虑其平衡性，不需要考虑其是不是排序二叉树

**平衡二叉树又称AVL树，它是一棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。**


<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>递归</div>

1. 找出左右子树的深度 
2. 判断深度差是否小于1

</fieldset>
</form>

## code2

``` bash 
class Solution {
public:
    bool status = true;
    bool IsBalanced_Solution(TreeNode* pRoot)
    {
       GetDeep(pRoot);
       return status;
    }  
    
    int GetDeep(TreeNode* pRoot){
       if(pRoot == NULL){
           return 0;
       }
       int leftDeep = GetDeep(pRoot->left);
       int rightDeep = GetDeep(pRoot->right);
       if(abs(leftDeep-rightDeep)>1){
            status = false;
       }
       return max(leftDeep,rightDeep)+1;
     }
};
```