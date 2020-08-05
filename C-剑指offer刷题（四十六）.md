---
title: C++剑指offer刷题（四十六）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-14 13:12:48
tags:
keywords: 链表环
description: 快慢指针
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
给一个链表，若其中包含环，请找出该链表的环的入口结点，否则，输出null。

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>快慢指针</div>

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@5.5/img/article/CPPoffer/listhuan.png" width =100% height = 100% />

1. 定义快慢指针（快指针一次走两步，慢指针一次走一步）
2. 找第一次相遇点，一定相遇在环内
3. 慢指针指向头指针
4. 快慢指针一次走一步，如果相等则说明再次相遇点是环的入口
5. 返回任意一个指针

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
};
*/
class Solution {
public:
    ListNode* EntryNodeOfLoop(ListNode* pHead)
    {
        if(pHead == NULL){
            return NULL;
        }
        ListNode* fast = pHead;
        ListNode* slow = pHead;
        //相遇点
        while(fast && fast->next){
            fast = fast->next->next;
            slow = slow->next;
            if(slow == fast){
                break;
            }
        }
        if(!fast || !fast->next){
            return NULL;
        }
        slow = pHead;
        while(fast!=slow){
            slow = slow->next;
            fast = fast->next;
        }
        return fast;
    }
};
```