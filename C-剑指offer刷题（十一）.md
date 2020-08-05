---
title: C++剑指offer刷题（十一）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-23 10:55:50
tags:
keywords: 链表
description: 链表查找、反转
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
### 链表查找
输入一个链表，输出该链表中倒数第k个结点。
<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>快慢指针</div>
1. 定义两个指针指向链表
2. front先向前移动k个单位
3. front 和 after同时向前移动
4. 直到front指向NULL
5. 返回after
<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@3.9/img/article/CPPoffer/lianbiao.png" width = 70% height = 35% />

</fieldset>
</form>

## 实现code

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
    ListNode* FindKthToTail(ListNode* pListHead, unsigned int k) {
        if(pListHead == NULL || k<1){
            return NULL;
        }
        ListNode* front = pListHead;
        ListNode* after = pListHead;
        while(k>0){
            if(front == NULL){ //当移动k时，链表不够长，返回NULL
                return NULL;
            }
            front = front->next;
            k--;
        }
        while(front!= NULL){
            front = front->next;
            after = after->next;
        }
        return after;
    }
};
```

### 链表反转

输入一个链表，反转链表后，输出新链表的表头。（反转链表也要输出）
<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>头插法</div>
1. 从原链表的头部一个一个取节点并插入到新链表的头部

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@3.9/img/article/CPPoffer/lianbiaofanzhuan.png" width = 70% height = 35% />

</fieldset>
</form>

### code
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
    ListNode* ReverseList(ListNode* pHead) {

        ListNode* reversal = NULL;
        ListNode* initial = pHead;
        if(pHead == NULL || pHead->next == NULL){
            return pHead;
        }
 
        while(initial != NULL){
            ListNode* next = initial->next;
            initial->next = reversal;  //反转
            reversal = initial;
            initial = next;
        }
        return reversal;
    }
};
```