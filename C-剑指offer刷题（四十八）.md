---
title: C++剑指offer刷题（四十八）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-15 19:34:51
tags:
keywords: 二叉树
description: 二叉树中序遍历的下一个节点
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
给定一个二叉树和其中的一个结点，请找出中序遍历顺序的下一个结点并且返回。注意，树中的结点不仅包含左右子结点，同时包含指向父结点的指针。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>特点</div>

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@5.6/img/article/CPPoffer/erchashunextnode.png" width =100% height = 100% />

1. 判断是否有右子树
2. 有右子树：下个结点就是右子树最左边的点（D，B，E，A，C，G）
3. 没有右子树：（1）这个节点是父节点左孩子（N，I，L）——父节点就是下一个节点
     &emsp;&emsp;&emsp; &emsp;&emsp;（2）这个节点是父节点右孩子（H，J，K，M）——找他的父节点的父节点的父节点...直到找的这个节点是他父节点的左孩子位置，如果没有，比如M，那么他就是尾节点。

</fieldset>
</form>

## code
``` bash
/*
struct TreeLinkNode {
    int val;
    struct TreeLinkNode *left;
    struct TreeLinkNode *right;
    struct TreeLinkNode *next;
    TreeLinkNode(int x) :val(x), left(NULL), right(NULL), next(NULL) {
        
    }
};
*/
class Solution {
public:
    TreeLinkNode* GetNext(TreeLinkNode* pNode)
    {
        if(pNode == NULL){
            return NULL;
        }
        //输入D 存在右孩子的时候，下一个节点就是找一直找左孩子
        if(pNode->right != NULL){
            pNode = pNode->right;
            while(pNode->left !=NULL){
                pNode = pNode->left;
            }
            return pNode;
        }
        //没有右孩子找父节点，只要父节点不为空一直遍历
        while(pNode->next !=NULL){
            //定义一个父节点
            TreeLinkNode* pRoot = pNode->next;
            //N是父节点的左孩子，返回父节点
            if(pRoot->left == pNode){
                return pRoot;
            }
            //.J是右孩子，一直找父节点的父节点
            pNode = pNode->next;
        }
        //其他情况返回NULL
        return NULL;
    }
};
```