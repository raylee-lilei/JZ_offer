---
title: C++剑指offer刷题（五十五）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-30 11:39:50
tags:
keywords: 中位数
description: 数据流中中位数 队列
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。我们使用Insert()方法读取数据流，使用GetMedian()方法获取当前读取数据的中位数。

<form action="" method="">
<fieldset><legend font-weight:600>思路一 :</legend>
<div align=“Center”>STL upper_bound()</div>

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@6.0/img/article/CPPoffer/upper_bound.png" width =100% height = 100% />
1. 插入数组时，使用upper_bound(),返回数组中最后一个大于等于num 的值
2. 找中位数如果为偶数返回中间两个值的平均
3. 如果为奇数，返回中间值

</fieldset>
</form>

<form action="" method="">
<fieldset><legend font-weight:600>思路二 :</legend>
<div align=“Center”>优先队列</div>
    priority_queue<int, vector<int>,greater<int>> right;//越小越优先[5,6,7] 拿出5 小根堆（数较大） 升序优先队列，优先删除最小 的
    priority_queue<int, vector<int>,less<int>> left; //越大越优先 [4,3,1]拿出4  大根 对（数较小）   降序    优先删除最大的


1. 将数组划分两个数组流
2. 先放入往左边数组放一个值 ，根据大小顶对的特点插入数据
3. 最终大根堆降序，小根堆升序
4. 取出中位数

</fieldset>
</form>

## code
``` bash
class Solution {
public:
#if 0
    vector<int> DataStream;
    void Insert(int num)
    {
        //使用STL中upper_bound(),返回数组中最后一个大于等于num 的值
        auto position = upper_bound(DataStream.begin(), DataStream.end(), num);
        DataStream.insert(position, num);
    }

    double GetMedian()
    { 
        int size = DataStream.size();
        if(size%2==0){
            return 1.0*(DataStream[size/2-1]+DataStream[size/2])/2;
        }else{
            return DataStream[size/2]*1.0;
        }
    }
#endif
    //[1,3,4,5,6,7]   [1,3,4]和[5,6,7]
    //优先队列
    priority_queue<int, vector<int>,greater<int>> right;//越小越优先[1,3,4] 拿出4
    priority_queue<int, vector<int>,less<int>> left; //越大越优先[5,6,7] 拿出5
    void Insert(int num)
    {
        left.push(num);
        if(left.size()-right.size()>1) {
			//从大根堆拿最大的元素在小根 堆中
            right.push(left.top());
            left.pop();
        }
        if(right.size()>0 && left.top()>right.top()){
            int tmp=left.top();
            left.pop();
            left.push(right.top());
            right.pop();
            right.push(tmp);
        }
    }

    double GetMedian()
    { 
        if(left.size()==right.size()) return 1.0*(left.top()+right.top())/2;
        else return left.top();
    }
};
```