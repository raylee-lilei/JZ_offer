---
title: C++剑指offer刷题（三十二）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-23 13:13:08
tags:
keywords: 链表
description: 链表公共节点
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---

## 题目描述
输入两个链表，找出它们的第一个公共结点。（注意因为传入数据是链表，所以错误测试数据的提示是用其他方式显示的，保证传入数据是正确的）

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>指针扫描</div>

1. 定义两个指针分别指向两个链表
2. 在p1 != p2 条件下
2. p1 指向空的时候，让他指向pHead2
3. p2 指向空的时候，让他指向pHead1，p1 ！=  p2 p1继续往下指，直到指向空
4. 两个指针分别向后指
5. 返回p1

</fieldset>
</form>

## code 
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
    ListNode* FindFirstCommonNode( ListNode* pHead1, ListNode* pHead2) {
        if(pHead1== NULL || pHead2 ==  NULL){
            return NULL;
        }
        ListNode *p1 = pHead1;
        ListNode *p2 = pHead2;
        while(p1!=p2){
            //p1 指向空的时候，让他指向pHead2
            p1 = (p1 == NULL ? pHead2 : p1->next );
            //p2 指向空的时候，让他指向pHead1，p1 ！=  p2 p1继续往下指，直到指向空
            p2 = (p2 == NULL ? pHead1 : p2->next );
        }
        return p1;
    }
};
```