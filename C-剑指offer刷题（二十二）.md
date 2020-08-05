---
title: C-剑指offer刷题（二十二）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-06 19:33:18
tags:
keywords: 二叉树转链表
description: 二叉树转链表
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>二叉树指针操作（中序遍历）</div>

1. 定义一个栈；定义一个指针pre记录上一次出栈值
2. 遍历左子树放入栈中
3. 取出栈顶元素就是最小值也是链表头结点
4. 出栈，第一次出栈，前一次指针pre为空；如果不为空穿线，pre后继直线当前位置，当前位置的前继指向pre的位置
5. pre指向当前位置
6. 继续遍历右子树

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@4.8/img/article/CPPoffer/erchashutolianbiao.png" width = 100% height = 70% />

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
    TreeNode* Convert(TreeNode* pRootOfTree)
    {
        if(pRootOfTree == NULL){
            return NULL;
        }
        
        TreeNode *head = NULL;
        TreeNode *pre = NULL;
        stack<TreeNode*> tempStack;
        
        while(pRootOfTree || !tempStack.empty()){
            //找到左子树的最小值并依次压栈
            while(pRootOfTree){
                tempStack.push(pRootOfTree);
                pRootOfTree = pRootOfTree->left;
            }
            //当前指针指向最小值
            if(!tempStack.empty()){
                pRootOfTree = tempStack.top();
                tempStack.pop();
                if(pre != NULL){
                    //pre的后继指向当前（最开始指向最小值）
                    pre->right = pRootOfTree;
                    //当前的前继指向pre
                    pRootOfTree->left = pre; 
                }else{
                    //返回头结点
                    head = pRootOfTree;
                }
            //pre向后移动
            pre = pRootOfTree;
            //找是否存在右子树
            pRootOfTree = pRootOfTree->right;
        }
     }
    return head;
    }
};
```