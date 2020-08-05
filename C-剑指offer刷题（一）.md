---
title: C++剑指offer刷题（一）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-13 19:45:49
tags:
keywords: 数组、搜索
description: 数组、搜索
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
&emsp;&emsp;在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
<html lang ="zh-CN">
<head></head><body>
<table width="30" height="150" border="1"><tr><td width="1" >1</td><td width="1" >2</td><td width="1" >3</td><td width="10" >4</td><td width="10" >5</td></tr><tr><td width="1" >6</td><td width="1" >7</td><td width="1" >8</td><td width="10" >9</td><td width="10" >10</td></tr><tr><td width="1" >11</td><td width="1" >12</td><td width="1" >13</td><td width="10" >14</td><td width="10" >15</td></tr><tr><td width="1" >16</td><td width="1" >17</td><td width="10" >18</td><td width="10" >19</td><td width="10" >20</td></tr><tr><td width="1" >21</td><td width="1" >22</td><td width="10" >23</td><td width="10" >24</td><td width="10" >25</td></tr></table></body></html>
&emsp;&emsp;例如以上一个5X5的二维数组从**左到右递增**，**从上到下递增**，假如target这个数是12，判断12 是否在这个二维数组中

### 思路：
确定右上角数的X、Y坐标。
&emsp;&emsp;如果target比右上角值大，肯定在下一行，行往下找。
&emsp;&emsp;如果target比右上角值小，肯定在最后一列的左边，列往左找。


### 实现Code：
``` bash
class Solution{
public:
    bool Find (int target, vector<vector<int> > array){
        //找到数组的行
        int rows = array.size();
        //找到数组的列
        int cols = array[0].size();
        //找到右上角的数的X Y坐标
        int rowX = 0;
        int rowY = cols-1;
        //数组范围内查找
        while(rowX < rows && 0 <= rowY){
            if(target > array[rowX][rowY]){
                rowX++;
            }else if(target < array[rowX][rowY]){
                rowY--;
            }else
                return true;
        }
        return false;
    }
};
```
**************
vecter 定义一个二维数组：
``` bash
vector<vector<int> > array
```
二维数组确定行列
``` bash
//行  把每一行看成一个整体
int rows = array.size();
//列  第一行的个数
int cols = array[0].size();
```
