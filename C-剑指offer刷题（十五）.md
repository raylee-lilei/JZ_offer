---
title: C++剑指offer刷题（十五）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-27 11:20:20
tags:
keywords: 矩阵
description: 矩阵顺时针旋转输出
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。
	例如，如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 
	则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.


<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@4.2/img/article/CPPoffer/xuanzhuanjuzheng.png" width = 70% height = 70% />

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>遍历</div>
1. 从左向右遍历
2. 从上向下遍历
3. 从右向左遍历
4. 从下向上遍历
5. 缩小一圈

</fieldset>
</form>


## code
``` bash 
class Solution {
public:
    vector<int> printMatrix(vector<vector<int> > matrix) {
        //矩阵的行列
        int rows = matrix.size();
        int  cols = matrix[0].size();
        vector<int> PrintArray;
        if(rows == 0||cols == 0){
            return PrintArray;
        }
        int top = 0;  int right = cols-1;  int bottom =rows-1; int left = 0;
        while (left <= right && top <= bottom){
        //从左到右
        for(int i= top;i<=right;++i){
            PrintArray.push_back(matrix[top][i]);
        }

        //从上到下
        for(int j =top+1;j<=bottom;++j){
            PrintArray.push_back(matrix[j][right]);
        }
        //从右到左
        if (top != bottom)
        for(int m =right-1;m >=left; --m){
             PrintArray.push_back(matrix[bottom][m]);
        }
        //从下到上
        if (left != right)
        for(int n = bottom-1;n>top;--n){
            PrintArray.push_back(matrix[n][left]);
        }
        ++top;
        --right;
        --bottom;
        ++left;
      }
    return PrintArray;
    }
};
```