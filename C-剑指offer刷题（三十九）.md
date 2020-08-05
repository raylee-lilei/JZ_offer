---
title: C++剑指offer刷题（三十九）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-29 10:12:44
tags:
keywords: 找顺子
description: 确定一个数组是否是顺子
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
LL今天心情特别好,因为他去买了一副扑克牌,发现里面居然有2个大王,2个小王(一副牌原本是54张^_^)...他随机从中抽出了5张牌,想测测自己的手气,看看能不能抽到顺子,如果抽到的话,他决定去买体育彩票,嘿嘿！！“红心A,黑桃3,小王,大王,方片5”,“Oh My God!”不是顺子.....LL不高兴了,他想了想,决定大\小 王可以看成任何数字,并且A看作1,J为11,Q为12,K为13。上面的5张牌就可以变成“1,2,3,4,5”(大小王分别看作2和4),“So Lucky!”。LL决定去买体育彩票啦。 现在,要求你使用这幅牌模拟上面的过程,然后告诉我们LL的运气如何， 如果牌能组成顺子就输出true，否则就输出false。为了方便起见,你可以认为大小王是0。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>顺子</div>
<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@5.4/img/article/CPPoffer/shunzi.png" width =100% height = 100% />

1. 统计0的个数
2. 统计间隙数
3. 如果0的个数大于等于间隙数，0可以填充在他们之间构成顺子，否则return  false。

</fieldset>
</form>

## code
``` bash 
class Solution {
public:
    bool IsContinuous( vector<int> numbers ) {
        if(numbers.size()<5){
            return false;
        }
        sort(numbers.begin(),numbers.end());
        int NumOfZero = 0, SpaceCount = 0;
            //统计0的个数
        for(int i = 0;i<numbers.size();++i ){
            if(numbers[i]== 0)NumOfZero++;
        }
           //统计间隙数
        for(int j = NumOfZero+1;j<numbers.size();j++){
            if(numbers[j]==numbers[j-1])return false;
            else{
                SpaceCount+= numbers[j]-numbers[j-1] -1;
            }
        }
        if(NumOfZero >= SpaceCount){
            return true;
        }else{
            return false;
        }
    }
};
```