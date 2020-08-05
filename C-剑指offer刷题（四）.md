---
title: C++剑指offer刷题（四）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-17 13:29:38
tag:
keywords: 树
description: 重构二叉树（前序中序）
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。

假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

### 先序遍历
先访问根，先序遍历左子树，左子树为空或者已遍历访问右子树

### 中序遍历
先访问左子树，左子树为空或者已遍历访问根，中序遍历右子树

### 后序遍历
后序遍历左子树，后序遍历右子树，左右子树为空或者已遍历才访问根

### 层次遍历
从根开始从左到右依次遍历

### 还原二叉树

**中序分左右 前序后序确定根**
<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@3.3/img/article/CPPoffer/fenxi.jpg" width = 70% height = 35% />
<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>还原二叉树实际上是递归的思想</div>
1.通过前序或者后序确定根
2.new一个还原后二叉树
&emsp;&emsp;&emsp;** TreeNode*  PTree = new TreeNode(Root);**
3.将前序和中序除了根以外的划分成左右子树分别存储在PreL、PreR、MidL、MidR中
4.递归构建二叉树的左右子树
</fieldset>
</form>


## 实现code
``` bash
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* reConstructBinaryTree(vector<int> pre,vector<int> vin) {
      if(pre.empty()||vin.empty()||pre.size()!=vin.size()){
          return NULL;
      }
      return Pre_Mid_ConstructBinaryTree(pre,vin);
}
      TreeNode*  Pre_Mid_ConstructBinaryTree(vector<int> &pre,vector<int> &mid){
          //确定根（前序遍历的第一个数就是根）
          int Root = pre[0];         
          //New一个重建二叉树
          TreeNode* PTree = new TreeNode(Root);
          
          //将中序遍历的结果分为左右两个部分放入vector中
          vector<int> MidL;
          vector<int> MidR;
          //前序遍历的结果从根之后开始依次是左子树和右子树，同样也单独存放在vector中
          vector<int> PreL;
          vector<int> PreR;
          int i = 0;int j =1;
          //分别找出前序和中序的左子树
          while(mid[i]!=Root){
             MidL.push_back(mid[i++]);
             PreL.push_back(pre[j++]);
          }
          //跳过中序遍历中的根
          ++i;
          //分别找出前序和中序的右子树
          while(i<mid.size()){
             MidR.push_back(mid[i++]);
             PreR.push_back(pre[j++]);
          }
          
          //构建左右子树
          if(!MidL.empty()&& !PreL.empty()){
             PTree->left = Pre_Mid_ConstructBinaryTree(PreL,MidL);
          }
          if(!MidR.empty()&& !PreR.empty()){
             PTree->right = Pre_Mid_ConstructBinaryTree(PreR,MidR);
          }
          return PTree;
      }
};
```
********
**● 使用指针还原前中序还原、后中序还原**

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@3.3/img/article/CPPoffer/erchashuhuanyuan.png" width = 55% height = 25% />
<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@3.3/img/article/CPPoffer/erchashuhuanzhizhenyuan.png" width = 55% height = 35% />

``` bash
//前序中序还原建立二叉树
TreeNode* pre_mid_createBiTree(char *pre,char *mid,int len) 
{
    if(len==0)
        return NULL;
    char ch=pre[0];  //找到先序中的第一个结点
    int index=0;
    while(mid[index]!=ch)//在中序中找到的根结点的左边为该结点的左子树，右边为右子树
    {
        index++;
    }
    TreeNode* T=new TreeNode(ch);//创建根结点
    T->data=ch;
    T->lchild=pre_mid_createBiTree(pre+1,mid,index);//建立左子树
    T->rchild=pre_mid_createBiTree(pre+index+1,mid+index+1,len-index-1);//建立右子树
    return T;
}


//后序中序还原建立二叉树
TreeNode* pro_mid_createBiTree(char *last,char *mid,int len)
{
    if(len==0)
       return NULL;
    char ch=last[len-1]; //取得后序遍历顺序中最后一个结点
    int index=0;//在中序序列中找根结点，并用index记录长度
    while(mid[index]!=ch)//在中序中找到根结点，左边为该结点的左子树，右边为右子树
       index++;
    TreeNode* T=new TreeNode(ch);;//创建根结点
    T->data=ch;
    T->lchild=pro_mid_createBiTree(last,mid,index);//建立左子树
    T->rchild=pro_mid_createBiTree(last+index,mid+index+1,len-index-1);//建立右子树
    return T;
}
```