---
title: C++剑指offer刷题（六）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-18 14:53:57
tags:
keywords: 队列、栈
description: 两个栈表示一个队列
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
<head>
<link rel="stylesheet" href="/css/teat.css">
</head>
## 题目描述
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。
**输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。**
*例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。*
*NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。*

<table><tr><td class="test">0</td><td class="test">1</td><td class="test">2</td><td class="test">3</td><td class="test">4</td><td class="test">5</td><td class="test">6</td><td class="test">7</td><td class="test">8</td><td class="test">9</td><td class="test">10</td><td class="test">11</td></tr></table>
&emsp;first**&darr;**&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;middle**&darr;**&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; end**&darr;**
<table><tr><td class="test">1</td><td class="test">2</td><td class="test">3</td><td class="test">4</td><td class="test">5</td><td class="test">6</td><td class="test">7</td><td class="test">8</td><td class="test">9</td><td class="test">10</td><td class="test">11</td><td class="test">12</td></tr></table>
&emsp;first**&darr;**&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;middle**&darr;**&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; end**&darr;**
<table><tr><td class="test">7</td><td class="test">8</td><td class="test">9</td><td class="test">10</td><td class="test">11</td><td class="test">12</td><td class="test">1</td><td class="test">2</td><td class="test">3</td><td class="test">4</td><td class="test">5</td><td class="test">6</td></tr></table>
&emsp;first**&darr;**&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;middle**&darr;**&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp; end**&darr;**
<table><tr><td class="test">3</td><td class="test">3</td><td class="test">4</td><td class="test">5</td><td class="test">5</td><td class="test">2</td><td class="test">2</td><td class="test">2</td><td class="test">2</td><td class="test">2</td><td class="test">2</td><td class="test">2</td></tr></table>

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>二分法查找</div>
由于数组是递增的，旋转之后实际上前一部分是递增的，后一部分也是递增的。
利用二分查找：
如果中间元素值大于最后一个元素值，说明最小值在右半区间，
如果中间元素值小于最后一个元素值，说明最小值在左半区间，或者min就是这个中间值
如果相等说明有相同元素，需要将判断区间往前缩一下，继续判断。
不断循环，当二分查找的的左右区间相等了，就说明找到最小值了。

</fieldset>
</form>

## 实现code
``` bash
class Solution {
public:
    int minNumberInRotateArray(vector<int> rotateArray) {
        if(rotateArray.size()==0){
            return 0;
        }
        //定义组数开始、中间、结尾的下标
        int first = 0;
        int end = rotateArray.size()-1;
        int middle = 0;
        
        while(first<end){
            middle = (first+end)/2;
            //当中间元素 大于 最后一个元素，说明最小值在右半区间 
            //此时缩小区间first 到 end
            if(rotateArray[middle]>rotateArray[end]){
                first +=1;
            }else if(rotateArray[middle]<rotateArray[end]){
                //当中间元素 小于 最后一个元素 ，说明最小值在右半区间，并且这个中间值也可能是最小值
                end = middle;
            }else{
                //中间元素 等于 最后一个元素，存在重复的元素，只能缩小一个范围
                end -=1;
            }
        }
        
        return rotateArray[first];
    }    
};

```