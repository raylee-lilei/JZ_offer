---
title: C++剑指offer刷题（三十一）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-23 13:12:49
tags:
keywords: 逆序对 
description: 归并排序
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组,求出这个数组中的逆序对的总数P。并将P对1000000007取模的结果输出。 即输出P%1000000007

### 归并排序
其实就是分治合并

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@5.2/img/article/CPPoffer/fenzhi.png" width =100% height = 100% />
<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@5.2/img/article/CPPoffer/guibing.png" width =100% height = 100% />

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>归并排序</div>

1. 分治（分成左右两边相等的两个数组，递归继续划分，直到只剩下数组只有 1个元素）
2. 合并排序，定义一个临时数组存放排序后的结果（在合并的过程中就能找出逆序对）
3. 主要是找 左边和右边  断开的逆序对
&emsp;&emsp;若果此时i 的值比j的值小，他们之间不构成逆序对，把最小的值放入临时数组中，并且指向i 的指针向后移动继续比较
&emsp;&emsp;若果发现此时i 的值比j 的值大，他们构成逆序对，并且他们之间有 （mid - i + 1）对
4. 判断前半部分
5. 判断后半部分
6. 排序好的覆盖原来的

</fieldset>
</form>

## code 
``` bash 
class Solution {
public:
    int count;
    int InversePairs(vector<int> nums) {
        if(nums.size()!=0){
            //分治   划分整个数组
            divide(nums ,0,nums.size()-1);
        }
        return count;
    }
    //分治思路
    void divide(vector<int> &nums,int start,int end){
        if(start >= end) return;
        //取中间值
        int mid = start + (end-start)/2;
        //递归左右两边数组   
        divide(nums,start,mid);
        divide(nums,mid+1,end);
        //合并排序
        merge(nums,start,mid,end);
    }
    
    //合并
    void merge(vector<int> &nums,int start ,int mid, int end){
        //定义临时数组
        vector<int> temp;
        int i = start , j = mid+1,k = 0;
        //比较左右两边间隙，中间存在逆序对 【start....i.....mid】【mid+1.....j.....end】
        while(i<=mid && j<=end){
            //若果此时i 的值比j的值小，他们之间不构成逆序对，把 最小的值放入临时数组中，并且指向i 的指针向后移动继续比较
            if(nums[i] <= nums[j]){
                temp.push_back(nums[i++]);
            }else{
                //若果发现此时i 的值比j 的值大，他们构成逆序对，并且他们之间有 （mid - i + 1）对
                temp.push_back(nums[j++]);
                count = (count + mid-i+1)%1000000007;
            }
        }
        //判断前半部分 
        while(i<=mid){
            temp.push_back(nums[i++]);
        }
        //判断后半部分
        while(j<=end){
            temp.push_back(nums[j++]);
        }
        //排序好的覆盖原来的
        for(k;k<temp.size();++k){
            nums[start+k] = temp[k];
        }
    }
    
};

```