---
title: C++剑指offer刷题（四十七）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-06-14 13:12:57
tags:
keywords: 链表 
description: 链表删除重复点
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->5

<form action="" method="">
<fieldset><legend font-weight:600>思路:</legend>
<div align=“Center”>特点</div>

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@5.5/img/article/CPPoffer/deletelistcopynode.png" width =100% height = 100% />

1. 定义三个指针分别指向头指正和NULL，
2. 在当前指针不为空的条件下遍历
3. 如果当前指针和指针指向的下一个相等，last 指向当前的下一个，否则，pre 指向当前指针，当前指针指向下一个
4. 若果当前指针和指针指向的下一个相等，继续 向下遍历判断last的值和当前的指针任然一样，则last往后移动，知道不等于当前指针的值
5. 若果当前指针和指针指向的下一个相等，last移动后的值已经不等于当前值了，此时我们要删除节点，如果当前指针指向头结点的话，我们要删除从头结点到last的下一个。如果 当前节点没有在头结点，我们删除pre的下一个到last的下一个
6. 更新当前指针，指向last的下一个位置
7. 返回此链表

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
};
*/
class Solution {
public:
    ListNode* deleteDuplication(ListNode* pHead)
    {
        ListNode* cur = pHead;
        ListNode* pre = NULL;
        ListNode* last = NULL;
        if(pHead == NULL){
            return NULL;
        }
        if(pHead->next ==NULL){
            return pHead;
        }
        while(cur!=NULL ){
            if(cur->next!= NULL && cur->next->val == cur->val){
               last = cur->next;
               while(last!=NULL && last->next!=NULL && last->next->val ==  cur->val ){
                   last = last->next;
               }
               if(cur == pHead){
                    pHead = last->next;
               }else{
                    pre->next = last->next;
               }
               cur = last->next;
                
            }else{
                 pre = cur;
                 cur = cur->next;
            }
        }
        return pHead;
    }
};
```