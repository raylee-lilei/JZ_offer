---
title: C++剑指offer刷题（十三）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-25 11:15:50
tags:
keywords: 二叉树
description: 二叉树遍历
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>二叉树递归</div>
1. 判断根节点是否相同
2. 若果不同，A的左子树与B的根比较；A的右子树与B的根比较
3. 判断是否是子结构
4. 检查A和B是否已经遍历完了
5. 不相等就返回false
6. 相等A和B的左子树是否相等，A和B的右子树是否相等，都相等B是A的子结构，否则不是

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
    bool HasSubtree(TreeNode* pRoot1, TreeNode* pRoot2)
    {
        //B为空不是子结构
        if(pRoot2 == NULL){
            return false;
        }
        //A为空肯定没有子结构
        if(pRoot1 == NULL){
            return false;
        }
        
        //判断第一个根节点是否相同
        bool flag = IsSubTree(pRoot1,pRoot2);
        
        //判断A的左子树有没有B子结构
        if(!flag){
           flag = HasSubtree(pRoot1->left,pRoot2); 
        }
          //判断A的右子树有没有B子结构
        if(!flag){
           flag = HasSubtree(pRoot1->right,pRoot2);
        }
        return flag;
    }    
    bool IsSubTree(TreeNode* pSub1,TreeNode* pSub2){
        
        //判断B中还是否有子树
        if(pSub2 == NULL){
            //B已经没有子树了，但是和A是相同的
            return true;
        }
        //A已经没有子树了，B还有，则B肯定不是A的子结构
        if(pSub1 == NULL){
            return false;
        }
        if(pSub1->val != pSub2->val){
            return false;
        }
        //继续遍历左右子树
        return IsSubTree(pSub1->left,pSub2->left) && IsSubTree(pSub1->right,pSub2->right);
    }

};
```