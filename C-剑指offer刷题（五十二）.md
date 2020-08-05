---
title: C++剑指offer刷题（五十二）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-20 12:58:20
tags:
keywords: 二叉树
description: 二叉树遍历
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
请实现两个函数，分别用来序列化和反序列化二叉树

二叉树的序列化是指：把一棵二叉树按照某种遍历方式的结果以某种格式保存为字符串，从而使得内存中建立起来的二叉树可以持久保存。序列化可以基于先序、中序、后序、层序的二叉树遍历方式来进行修改，序列化的结果是一个字符串，序列化时通过 某种符号表示空节点（#），以 ！ 表示一个结点值的结束（value!）。

二叉树的反序列化是指：根据某种遍历顺序得到的序列化字符串结果str，重构二叉树。

例如，我们可以把一个只有根节点为1的二叉树序列化为"1,"，然后通过自己的函数来解析回这个二叉树

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>二叉树遍历</div>

1. 序列化（树——>字符串）
2. char——>string
3. 如果为空res = '#'
4. 如果不为空，每个树节点之后加上字符","
5. 遍历左子树
6. 遍历右子树
7. 反序列化（字符串——>树）
8. 计算下每个节点字符的长度
9. 判断字符是否为空
10. 定义一个符号位
11. 如果字符串中遇到"-"符号位= -1
12. 计数指针向后移动一位
13. 将每个节点的字符转成数字
14. 数字乘上符号位
15. 计数指针往后移动判断下一个节点的数字
16. 生成二叉树（递归反序列化左子树、右子树）


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
    char* Serialize(TreeNode *root) { 
        string res;
        //深度优先遍历算法
        DFS1(root,res);
        //string  转 char
        char* p = new char[res.size()];
        strcpy(p, res.c_str());
        return p;
    }
    //二叉树序列化
    void DFS1(TreeNode *root,string &res){
        //遍历到空节点
        if(!root){
            res += "#,";
            return;
        }
        //非空节点
        res += to_string(root->val) + ",";
        DFS1(root->left, res);
        DFS1(root->right, res);
        
    }
    //反序列化
    TreeNode* Deserialize(char *str) {
        int index = 0;
        return DFS2(str,index);
    }
    //index 字符串串长度
    TreeNode* DFS2(char *str,int &index){
        //确定每个数字 长度  135长度为3   3 长度1
        int len = index;
        while(str[len] != ','){
            len++;
        }
        //空节点
        if(str[index]=='#'){
            index = len+1;
            return NULL;
        }
        //非空节点
        int num = 0;
        //符号
        int sign = 1;
        if(index<len && str[index] == '-'){
            sign = -1;
            index++;
        }
        for(int i = index;i<len;++i){
            num = num *10 + str[i] - '0';
        }
        num *= sign;
        //index往下走
        index = len+1;
        
        auto root = new TreeNode(num);
        root->left = DFS2(str,index);
        root->right = DFS2(str,index);
        return root;
    }

};
```