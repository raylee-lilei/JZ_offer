---
title: C++剑指offer刷题（四十九）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-17 21:13:44
tags:
keywords: 二叉树
description: 二叉树层次遍历
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述1
请实现一个函数按照之字形打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右至左的顺序打印，第三行按照从左到右的顺序打印，其他行以此类推。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>层次遍历（之）  栈</div>

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@5.8/img/article/CPPoffer/erchashuzhiprint.png" width =100% height = 100% />

1. 定义两个栈存放每一层数
2. 定义一个指针每次指向栈顶元素
3. 先把根存放在栈1中
4. 在栈1不为空的条件下遍历（奇数行从左到右）
5. 栈1出栈，使用栈顶指针去找左右子树，分别压栈，存放在数组中
6. 栈1存放奇数行，栈2存放偶数行
7. 一层遍历完之后把每一层的结果放入Result中，并清除临时数组
8. 在栈2不为空的条件下遍历（偶数行从右到左）
9. 栈2出栈，使用栈顶指针去找左右子树，分别压栈，存放在数组中
10. 一层遍历完之后把每一层的结果放入Result中，并清除临时数组
11. 返回Result

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
};
*/
class Solution {
public:
    vector<vector<int> > Print(TreeNode* pRoot) {
        vector<vector<int> > Result;
        if(pRoot == NULL){
            return Result;
        }
        vector<int> Temp;
        stack<TreeNode*> Stack1;
        stack<TreeNode*> Stack2;
        TreeNode* MoveNode = NULL;
        
        Temp.push_back(pRoot->val);
        Result.push_back(Temp);
        Temp.clear();
        Stack1.push(pRoot);
        
        while(!Stack1.empty() || !Stack2.empty()){
            while(!Stack1.empty()){
                MoveNode = Stack1.top();
                Stack1.pop();
                if(MoveNode->right){
                    Stack2.push(MoveNode->right);
                    Temp.push_back(MoveNode->right->val);
                }
                if(MoveNode->left){
                    Stack2.push(MoveNode->left);
                    Temp.push_back(MoveNode->left->val);
                }
            }
            if(!Temp.empty()){
                Result.push_back(Temp);
                Temp.clear();
            }
            
            while(!Stack2.empty()){
                MoveNode = Stack2.top();
                Stack2.pop();
                if(MoveNode->left){
                    Stack1.push(MoveNode->left);
                    Temp.push_back(MoveNode->left->val);
                }
                if(MoveNode->right){
                    Stack1.push(MoveNode->right);
                    Temp.push_back(MoveNode->right->val);
                }
            }
            if(!Temp.empty()){
                Result.push_back(Temp);
                Temp.clear();
            }
        }
        return Result;
    }
    
};
```

## 题目描述2
从上到下按层打印二叉树，同一层结点从左至右输出。每一层输出一行。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>层次遍历  队列</div>

1. 定义一个队列和一个指针指向队列的头部 
2. 先把根存放在队列中
3. 在队列不为空的条件下遍历
4. 定义一个临时数组
5. 出队列
6. 把指针指向的值存放在临时数组中
7. 找指针的左右子树，放入队列中
8. 一层遍历完之后，把临时数组放入Result中
9. 返回Result

</fieldset>
</form>

## code2
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