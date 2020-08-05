---
title: C++剑指offer刷题（十二）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-24 12:51:50
tags:
keywords: 链表
description: 链表合并
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述

输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

<form action="" method="">
<fieldset><legend font-weight:600>思路1：</legend>
<div align=“Center”>链表指针</div>
1. 定义一个新的链表，确定头结点
2. 比较大小，穿线
3. 链表指针向后移动，合并链表指针也向后移动
4. 如果输入链表长度不一致
5. 一个为空之后直接返回另一个
<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@4.0/img/article/CPPoffer/lianbiaomerge.png" width = 100% height = 100% />

</fieldset>
</form>

## code1
``` bash
/*
struct ListNode {
	int val;
	struct ListNode *next;
	ListNode(int x) :
			val(x), next(NULL) {
	}
};*/
class Solution {
public:
    ListNode* Merge(ListNode* pHead1, ListNode* pHead2)
    {
        if(!pHead1){
            return pHead2;
        }
        if(!pHead2){
            return pHead1;
        }
        
        ListNode* newList  = NULL;
        //拿出一个小的值作为头结点
        if(pHead1->val<=pHead2->val){
            newList = pHead1;
            pHead1 = pHead1->next;
        }else{
            newList = pHead2;
            pHead2 = pHead2->next;
        }
        ListNode* newListP  = newList;
        while(pHead1 && pHead2){
          if(pHead1->val<=pHead2->val){
             newListP->next = pHead1;//穿线 
             pHead1 = pHead1->next;//第一个指针向后移
             newListP = newListP->next;//合并后的指针也向后移动
          }else{
             newListP->next = pHead2;//穿线
             pHead2 = pHead2->next;//第二个指针向后移
             newListP = newListP->next; 
           }
         }
        //如果两个链表长度不一样
        if(pHead1 == NULL){
            newListP->next = pHead2;
        }
        if(pHead2==NULL){
            newListP->next = pHead1;
        } 
       return newList;
   }
};
```

<form action="" method="">
<fieldset><legend font-weight:600>思路2：</legend>
<div align=“Center”>递归法</div>
1. 定义一个新的链表
2. 比较大小,较小的依次放入newList
3. newList下一个用未比较的继续比较，较小的依次放入newList

</fieldset>
</form>


## code 
```bash
/*
struct ListNode {
	int val;
	struct ListNode *next;
	ListNode(int x) :
			val(x), next(NULL) {
	}
};*/
class Solution {
public:
    ListNode* Merge(ListNode* pHead1, ListNode* pHead2)
    {
        if(!pHead1){
            return pHead2;
        }
        if(!pHead2){
            return pHead1;
        }
        ListNode* newList  = NULL;
        
        if(pHead1->val<=pHead2->val){
            newList = pHead1;
            newList->next = Merge(pHead1->next,pHead2);
        }else{
            newList = pHead2;
            newList->next = Merge(pHead1,pHead2->next);
        }
       return newList;
   }
};
```