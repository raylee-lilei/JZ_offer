---
title: C++剑指offer刷题（五十八）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-30 11:40:09
tags:
keywords: 数组
description: 二维数组中移动
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
地上有一个m行和n列的方格。一个机器人从坐标0,0的格子开始移动，每一次只能向左，右，上，下四个方向移动一格，但是不能进入行坐标和列坐标的数位之和大于k的格子。 例如，当k为18时，机器人能够进入方格（35,37），因为3+5+3+7 = 18。但是，它不能进入方格（35,38），因为3+5+3+8 = 19。请问该机器人能够达到多少个格子？

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>回溯</div>

1. 定义有一个和矩阵一样的一维数组，初始化为0
2. 首先要判断上下左右是否划出了边界 
3. 数位值之和大于阈值，已近走过
4. 递归找这个值上下左右的位置，满足条件计数加一

</fieldset>
</form>

## code
``` bash
class Solution {
public:
    int movingCount(int threshold, int rows, int cols)
    {
        //定义 一个二维矩阵记录标记
        vector<vector<int>> flag(rows);  //行
        for(int i =0;i<rows;i++){   //列
            flag[i].resize(cols);
        }
        
        return DFS(threshold, rows, cols,flag,0,0);
    }
    
    int DFS(int threshold, int rows, int cols,vector<vector<int>> &flag,int i,int j){
        if(i<0 || i>=rows ||j<0 || j>=cols || CountSum(i)+CountSum(j) > threshold || flag[i][j]== 1){
            return 0;
        }
        flag[i][j]= 1;
        return 1
               +DFS(threshold,rows, cols,flag,i-1,j)
               +DFS(threshold,rows, cols,flag,i+1,j)
               +DFS(threshold,rows, cols,flag,i,j-1)
               +DFS(threshold,rows, cols,flag,i,j+1);
               
    }
    int CountSum(int i){
        int sum = 0;
        while(i>0){
            sum += i % 10;
            i /= 10;
        }
        return sum;
    }
};
```