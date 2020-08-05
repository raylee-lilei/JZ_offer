---
title: C++剑指offer刷题（十八）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-30 13:45:17
tags:
keywords: 二叉树、队列
description: 二叉树层次遍历
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
从上往下打印出二叉树的每个节点，同层节点从左至右打印。

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>借助一个辅助队列</div>
1. 把二叉树存放在队列里面
2. 队列的front的值放入vector中
3. 如果左子树为真，左子树放入vector中
4. 如果右子树为真，右子树放入vector中
5. 出队列
6. 返回PrintTreeNode打印出节点
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
    vector<int> PrintFromTopToBottom(TreeNode* root) {
        vector<int> PrintTreeNode;
        //辅助队列
        queue<TreeNode*> TempQueue;
        if(root == NULL){
            return PrintTreeNode;
        }
        TempQueue.push(root);
        while(!TempQueue.empty()){
            PrintTreeNode.push_back(TempQueue.front()->val);
            if(TempQueue.front()->left){
                TempQueue.push(TempQueue.front()->left);
            }
            if(TempQueue.front()->right){
                TempQueue.push(TempQueue.front()->right);
            }
            TempQueue.pop();
        }
        return PrintTreeNode;
    }
};
```