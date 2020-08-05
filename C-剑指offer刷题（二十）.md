---
title: C++剑指offer刷题（二十）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-02 17:18:04
tags:
keywords: 二叉树
description: 二叉树路径
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
输入一颗二叉树的根节点和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。
路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>先序遍历、递归</div>
1. 定义一个临时数组存储路径 ； 一个返回二维存放路径（全局变量）
2. 把根的值放入tempArray，判断是否与输入整数相等，是否为叶节点
3. 若果不满足，递归判断左子树，直到叶节点

	 if(root ==NULL){
            return Path;
        }

4. 删除最后一个叶节点（即回到上一个节点）继续递归右子树
     if(tempArray.size()!= 0){
            tempArray.pop_back();
        }

5. 重复3——4步骤，直到所有路劲遍历完
6. 返回满足条件的path

第一次遍历 22,10,4 &emsp;&emsp;&emsp;&emsp;36！=40，因此回退到父节点10上，开始寻找右孩子。

第二次遍历 22,10,8 &emsp;&emsp;&emsp;&emsp;40=40，此时正好输出这条路径（将路径添加到Path中），回退到父节点10上，此时10的左右孩子都已遍历完成，因此回退到父节点22

第三次遍历 22,13,5 &emsp;&emsp;&emsp;&emsp;40=40，此时正好输出这条路径（将路径添加到Path中）.

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@4.6/img/article/CPPoffer/erchashuPath.png" width = 100% height = 100% />

</fieldset>
</form>


## code 
``` bash
#include<iostream>
#include<vector>
using namespace std;

struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};

class Solution {
private:
    vector<int> tempArray;
    vector<vector<int>> Path;
public:
    vector<vector<int>> FindPath(TreeNode* root,int expectNumber) {
        
        if(root ==NULL){
            return Path;
        }
        tempArray.push_back(root->val);
        
        if(root->val == expectNumber&& root->left ==NULL && root->right == NULL){
            Path.push_back(tempArray);
        }

        if(root->val !=expectNumber && root -> left != NULL ){
            FindPath(root->left,expectNumber-root->val);
        }
        if(root->val!=expectNumber && root->right !=NULL){
              FindPath(root->right,expectNumber-root->val);
        }

        if(tempArray.size()!= 0){
            tempArray.pop_back();
        }
        return Path;
    }
};

int main()
{  
	//构建二叉树
	Solution tree;
	vector<vector<int> > result;
	TreeNode* root = new TreeNode(22);
	root->left = new TreeNode(10);
	root->right = new TreeNode(13);
	root->right->right = new TreeNode(5);
	root->left->left = new TreeNode(4);
	root->left->right = new TreeNode(8);
	
	result = tree.FindPath(root, 40);

	for (int i = 0; i < result.size(); i++)
	{
		for (int j = 0; j < result[i].size(); j++)
		{
			cout << result[i][j] << " ";
		}
		cout << endl;
	}
	return 0;
}
```

