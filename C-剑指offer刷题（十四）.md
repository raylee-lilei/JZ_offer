---
title: C++剑指offer刷题（十四）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-26 11:09:35
tags:
keywords: 二叉树
description: 二叉树镜像
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
操作给定的二叉树，将其变换为源二叉树的镜像。

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@4.1/img/article/CPPoffer/erchashumirrorT.png" width = 100% height = 100% />

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>递归</div>
1. 交换根的左右子树
2. 递归交换子树的左右子树

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@4.1/img/article/CPPoffer/erchashumirror.png" width = 100% height = 100% />

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
};*/
class Solution {
public:
    void Mirror(TreeNode *pRoot) {
        if(!pRoot){
            return;
        }
        TreeNode* tempTree = pRoot->left;
        pRoot->left = pRoot->right;
        pRoot->right = tempTree;
        
        //递归左子树
        Mirror(pRoot->left);
        //递归右子树
        Mirror(pRoot->right);
    }
};
```