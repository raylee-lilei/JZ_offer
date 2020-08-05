---
title: C++剑指offer刷题（三）
author: raylee
avatar: 'https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.4/img/custom/logo_1.png'
authorLink: 
authorAbout: industry pays
authorDesc: industry pays
categories: technology
comments: true
date: 2020-04-16 10:20:57
tag:
keywords: 链表
description: 链表逆序
photos: https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@2.0/img/cover/03.jpg.webp
---
<head>
<link rel="stylesheet" href="/css/teat.css">
</head>

## 题目描述
输入一个链表，按链表从尾到头的顺序返回一个ArrayList。

<form action="" method="">
<fieldset><legend font-weight:600>思路1：</legend>
<div align=“Center”>借助栈stack先进后出反弹至vector中</div>
1.定义一个链表指针指向输入的链表 保存链表类型的地址。
2.遍历输入的链表，依次压栈。
3.每次取出栈顶元素放入vector容器中。
4.出栈
</fieldset>
</form>


## 实现code1
``` bash
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        //借助栈
        //创建一个链表指针指向输入的链表
        ListNode *p =NULL;
        p = head;
        
        stack<int> TempStack; //定义一个栈
        vector<int> ArrayList; //定义一个vector容器
        while(p!=NULL){
            //压栈
            TempStack.push(p->val);
            p=p->next;
        }
        while(!TempStack.empty()){
            //把出栈的值放到vector容器中也就是返回的ArrayList
            ArrayList.push_back(TempStack.top());//栈顶的元素放到ArrayList中
            //出栈
            TempStack.pop();  
        }
        return ArrayList;
        
    }
};
```

<form action="" method="">
<fieldset><legend font-weight:600>思路2：</legend>
<div align=“Center”><p style="font-size:bold">使用反向迭代器</p>所有容器都定义了 begin 和 end 成员，分别返回指向容器首元素和尾元素下一位置的迭代器。容器还定义了 rbegin 和 rend 成员，分别返回指向容器尾元素和首元素前一位置的反向迭代器，如下图所示：

<img src="https://cdn.jsdelivr.net/gh/raylee-lilei/cdn@3.2/img/article/CPPoffer/iterator.gif">
</div>
1.遍历链表内容存放到vector容器中。
2.使用反向迭代器直接返回。
</fieldset>
</form>

## 实现code2
``` bash 
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {       
        vector<int> ArrayList; //定义一个vector容器
        //创建一个链表指针指向输入的链表
        ListNode *p =NULL;
        p = head;
        while(p!=NULL){
            ArrayList.push_back(p->val);
            p = p->next;
        }
		//返回一个反向迭代器
        return vector<int>(ArrayList.rbegin(),ArrayList.rend());        
    }
};

```