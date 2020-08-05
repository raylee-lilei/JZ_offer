---
title: C++剑指offer刷题（三十六）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-27 20:10:21
tags:
keywords: 数组
description: 数组中找出想要的数
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck!

输出所有和为S的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>大小指针移动</div>

1. 在两个指针内等差数列求和 
2. 如果和比输入数小，大指针向后移（先加上大的）
3. 相等的话依次将数插入数组中
4. 再把数组序列插入结果中，小指针继续加加，向后找
5. 如果和比输入数大，小指针向后移（先减去小的）

</fieldset>
</form>

## code
``` bash
class Solution {
public:
    vector<vector<int> > FindContinuousSequence(int sum) {
       vector<vector<int> >result;
        int small=1,big=2;
        while(small<big){
            int cur=(small+big)*(big-small+1)/2;
            if(cur<sum) big++;
            else if(cur==sum){
                vector<int> temp;
                for(int i=small;i<=big;i++){
                    temp.push_back(i);
                }
                result.push_back(temp);
                small++;
            }
            else small++;
        }
        return result;
    }
};
```

## 题目描述
输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。
对应每个测试案例，输出两个数，小的先输出。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>头尾指针移动</div>
实际上排序好的数列里，相差越远，他们乘积也就越小，头尾指针相差最远，依次缩小找到满足条件的就是最小的

1. 在头尾指针里面
2. 如果相等，直接把头尾指针放到数组中输出
3. 如果比输入值小，头指针向后移动 
4. 如果比输入值大，尾指针向前移动

</fieldset>
</form>

## code 
``` bash 
class Solution {
public:
    vector<int> FindNumbersWithSum(vector<int> array,int sum) {
        vector<int> result;
        if(array.size() == 0 ){
            return result;
        }
        int leftP = 0;
        int rightP = array.size()-1;
        while(leftP < rightP){
            int toltal = array[leftP]+array[rightP];
            if(toltal == sum){
                result.push_back(array[leftP]);
                result.push_back(array[rightP]);
                break;
            }else if(toltal < sum){
                ++leftP;
            }else{
                --rightP;
            }
        }
        return result;
    }
};
```