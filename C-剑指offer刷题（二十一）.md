---
title: C-剑指offer刷题（二十一）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-05-05 11:57:10
tags:
keywords: 链表
description: 链表复制
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
## 题目描述
输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针random指向一个随机节点），请对此链表进行深拷贝，并返回拷贝后的头结点。
注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空

<form action="" method="">
<fieldset><legend font-weight:600>思路：</legend>
<div align=“Center”>链表指针操作</div>

1. 复制一个与前一个值相同的结点
2. 穿线链接成一个新的链表
3. 设置新链表的随机指针作用域
	pClone->random =pNode->random->next;
4. 指向新链表的第二个结点即拷贝好的链表的头结点
5. 穿线操作拆分成两个链表（复制和被复制）

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@4.7/img/article/CPPoffer/copylianbiao.png" width = 100% height = 70% />

</fieldset>
</form>

## code
``` bash
/*
struct RandomListNode {
    int label;
    struct RandomListNode *next, *random;
    RandomListNode(int x) :
            label(x), next(NULL), random(NULL) {
    }
};
*/
class Solution {
public:
    RandomListNode* Clone(RandomListNode* pHead)
    {
        if(pHead == NULL){
            return NULL;
        }
        //复制链表节点并连线
        CloneNodeConnect(pHead);
        //新结点设置随机指针
        SetNodeRandom(pHead);
        //把链表从新拆分成两个链表
        return ReConnect(pHead);
    }
    
    void CloneNodeConnect(RandomListNode* Head){
        RandomListNode *pNode = Head;
        while(pNode != NULL){
            RandomListNode *pClone = new RandomListNode(pNode->label);
            pClone->next = pNode->next;
            pNode->next = pClone;
            pNode = pClone->next;
            
        }
    }
    
    void SetNodeRandom(RandomListNode* Head){
        RandomListNode *pNode = Head;
        while(pNode != NULL){
            RandomListNode *pClone = pNode->next;
            if(pNode->random){
                pClone->random =pNode->random->next;  
            }
            pNode = pClone->next;
        }
    }
    
    RandomListNode* ReConnect(RandomListNode* Head){
        RandomListNode* pNode = Head;
        //返回头结点
        RandomListNode* pCloned = Head->next;
        while(pNode != NULL){
            RandomListNode* pClone = pNode->next;
            //重连原链表
            pNode->next = pClone->next;
            pNode = pNode->next;
            if(pNode != NULL){
                //重连新链表
                pClone->next = pNode->next;
            }
        }
        return pCloned;
        
    }
};
```