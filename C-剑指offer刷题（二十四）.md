---
title: C-剑指offer刷题（二十四）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-11 12:30:08
tags:
keywords: 数组查找
description: 查找数组中超过长度一半的值
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。
例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。

<form action="" method="">
<fieldset><legend font-weight:600>思路1：</legend>
<div align=“Center”>sort排序</div>
1. 找数（中间的值即为所求）
2. 遍历计算计数
3. 判断是否满足条件

</fieldset>
</form>

## code1
```bash
class Solution {
public:
    int MoreThanHalfNum_Solution(vector<int> numbers) {      
        if(numbers.empty()){
            return 0;
        }
        //排序 如果满足条件，中间的值即为所求
        sort(numbers.begin(),numbers.end());
        int numSize = numbers.size();
        int halfNumSize = numSize >> 1;
        int middle = numbers[halfNumSize];
        
        //遍历计算计数
        int count = 0;
        for(auto x : numbers){
            if(middle == x){
                ++count;
            }
        }
        return (count > halfNumSize) ? middle : 0;
    }
};
```

<form action="" method="">
<fieldset><legend font-weight:600>思路2：</legend>
<div align=“Center”>数组规律</div>
1. 找数（如果有符合条件的数字，则它出现的次数比其他所有数字出现的次数和还要多）
&emsp;&emsp;&emsp;1.当前值与遍历值比较，如果相等计数加一
&emsp;&emsp;&emsp;2.不相等
&emsp;&emsp;&emsp;&emsp;&emsp;（1）判断count是否大于0
&emsp;&emsp;&emsp;&emsp;&emsp;（2）count大于0， - -count
&emsp;&emsp;&emsp;&emsp;&emsp;（2）count小于等于0 count置1并且当前值改为遍历值
	
2. 重新计算count的值
3. 判断是否满足条件

</fieldset>
</form>

## code2
``` bash
class Solution {
public:
    int MoreThanHalfNum_Solution(vector<int> numbers) {
        if(numbers.empty()){
            return 0;
        }
        int curVal,count = 0;
        int numSize = numbers.size();
        int halfNumSize = numSize >> 1;
        //int boundary = numSize >> 1;
        //作用就是迭代容器中所有的元素，每一个元素的临时名字就是x，等同于
        //for (vector<int>::iterator iter = nums.begin(); iter != nums.end(); iter++)
        //找出这个数字(如果有符合条件的数字，则它出现的次数比其他所有数字出现的次数和还要多)
        for(auto x : numbers){
            //如果相等计数加一
            if(curVal == x){
                ++count;
            }else{ //不相等继续判断，如果count不等于0，计数减一
                if(count>0){
                    --count;
                }else{//如果等于0 ，curVal当前值存放下一个值，并且把count置1
                    curVal=x;
                    count=1;
                }
            }
        }
        //重新计算count的值，来判断是否满则条件
        for(auto x : numbers){
            if(curVal == x){
                ++count;
            }
        }
        return (count > halfNumSize) ? curVal : 0;
    }
};
```