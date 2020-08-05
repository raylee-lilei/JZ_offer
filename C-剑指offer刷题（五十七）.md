---
title: C++剑指offer刷题（五十七）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-30 11:40:03
tags:
keywords: 矩阵
description: 矩阵字符串路径、回溯
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一个格子开始，每一步可以在矩阵中向左，向右，向上，向下移动一个格子。如果一条路径经过了矩阵中的某一个格子，则该路径不能再进入该格子。 例如【a&emsp; b&emsp;  c&emsp; e  &emsp;&emsp;&emsp;s&emsp; f &emsp; c &emsp;s &emsp;&emsp;&emsp; a&emsp; d&emsp; e&emsp; e】矩阵中包含一条字符串"bcced"的路径，但是矩阵中不包含"abcb"路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入该格子。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>回溯</div>
        //矩阵是一维的[a b c e   s f c s   a d e e] 
        //字符串一维 b c c e d 
        //找一个标志位实际上是和矩阵一样的一个数组  用来判断是否走过  0  未走过  1  表示走过

1. 定义有一个和矩阵一样的一维数组，初始化为0
2. 遍历矩阵，找字符串第一个在矩阵中的位置（首先要判断上下左右是否划出了边界）
3. 修改标志位的值，表示这个位置已经走过
4. 判断下str下一个是否是最后一个
5. 找这个值上下左右的位置
6. 没找到这个字符的上下左右是字符串中的路径，当前值变为未走过，继续去找下一个

</fieldset>
</form>

## code
``` bash
class Solution {
public:
    bool hasPath(char* matrix, int rows, int cols, char* str)
    {
        //矩阵是一维的[a b c e   s f c s   a d e e] 
        //字符串一维 b c c e d 
        //找一个标志位实际上是和矩阵一样的一个数组  用来判断是否走过  0  未走过  1  表示走过
        vector<char> flag(rows*cols,0);
        bool Result = false;
        //遍历矩阵
        for(int i = 0;i < rows;++i){
            for(int j = 0;j< cols;++j){
                Result = (Result || IsPath(matrix,flag,i,j,str,rows,cols));
            }
        }
        return Result;
    }
    
    bool IsPath(char* matrix,vector<char> flag,int x,int y,char *str,int rows, int cols){
        //判断是否溢出了矩阵的边界
        if(x<0 || x>= rows || y<0 || y>=cols){
            return false;
        }
        //找字符串第一个在矩阵中的位置
        if(matrix[x*cols+y] == *str && flag[x*cols+y] == 0){
            //修改标志位的值，表示这个位置已经走过
            flag[x*cols+y] = 1;
            //判断下str 是否是最后一个
            if(*(str+1)==0){
                return true;
            }
            //找这个值上下左右的位置
            bool Result = IsPath(matrix,flag,x,y+1,str+1,rows,cols) ||  
                          IsPath(matrix,flag,x-1,y,str+1,rows,cols) ||
                          IsPath(matrix,flag,x+1,y,str+1,rows,cols) ||
                          IsPath(matrix,flag,x,y-1,str+1,rows,cols);
            //没找到这个字符的上下左右是字符串中的路径，当前值变为未走过
            if(Result == false){
                 flag[x*cols+y] = 0;
            }
            return Result;
         }else{
            return false;
        }
    }

};
```