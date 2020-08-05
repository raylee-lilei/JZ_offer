---
title: C++剑指offer刷题（五十一）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-20 12:58:12
tags:
keywords: 二叉树
description: 二叉树层次遍历
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
从上到下按层打印二叉树，同一层结点从左至右输出。每一层输出一行。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>二叉树层次遍历</div>


1. 定义一个队列和一个指向队列头的指针
2. 往队列里面添加树根
3. 在队列不为空的条件下，定义一个临时数组
4. 队列出队
5. 向临时数组中添加指针指向的值
6. 遍历每一层，将 每一层的值插入队列中
7. 每一层的值放入Result中
8. 返回Result

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
        vector<vector<int> > Print(TreeNode* pRoot) {
            vector<vector<int>> Result;
            if(pRoot == NULL){
                return Result;
            }
            TreeNode* MoveNode = NULL;
            queue<TreeNode*> queTree;
            queTree.push(pRoot);
            while(!queTree.empty()){
                int size = queTree.size();
                vector<int> temp;
                while(size--){
                    MoveNode = queTree.front();
                    queTree.pop();
                    temp.push_back(MoveNode->val);
                    if(MoveNode->left!=NULL){
                        queTree.push(MoveNode->left);
                    }
                    if(MoveNode->right!=NULL){
                        queTree.push(MoveNode->right);
                    }
                }
                Result.push_back(temp);
            }
            return Result;
        
        }
};
```