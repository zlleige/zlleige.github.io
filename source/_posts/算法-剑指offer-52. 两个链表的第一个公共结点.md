---
title: 剑指offer——52. 两个链表的第一个公共结点
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 52. 两个链表的第一个公共结点

[NowCoder](https://www.nowcoder.com/practice/6ab1d9a29e88450685099d45c9e31e46?tpId=13&tqId=11189&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/5f1cb999-cb9a-4f6c-a0af-d90377295ab8.png" width="500"/> </div><br>

## 解题思路

设 A 的长度为 a + c，B 的长度为 b + c，其中 c 为尾部公共部分长度，可知 a + c + b = b + c + a。

当访问链表 A 的指针访问到链表尾部时，令它从链表 B 的头部重新开始访问链表 B；同样地，当访问链表 B 的指针访问到链表尾部时，令它从链表 A 的头部重新开始访问链表 A。这样就能控制访问 A 和 B 两个链表的指针能同时访问到交点。

```java
#if 1
/*
用一个set<ListNode* > 存两个链表的值，当插入值存在 则返回
时间复杂度O(2n) 空间复杂度O(2n)
*/
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *findFirstCommonNode(ListNode *headA, ListNode *headB) {
        if(!headA || !headB) return nullptr;
        set<ListNode* > s;
        ListNode* pA = headA;
        ListNode* pB = headB;
        //装载数据
        while(pA) 
        {
            s.emplace(pA), pA = pA ->next;
        }
        while(pB) 
        {
            if(! s.emplace(pB).second ) return pB;
            pB = pB ->next;
        }
        return nullptr;
    }
};

#endif

#if 0
/*
用两个栈 分别装入A B，然后再弹出，直到top不相等 
时间复杂度O(3n) 空间复杂度O(2n)
*/
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *findFirstCommonNode(ListNode *headA, ListNode *headB) {
        if(!headA || !headB) return nullptr;
        stack<ListNode* > sA;
        stack<ListNode* > sB;
        ListNode* pA = headA;
        ListNode* pB = headB;
        //装载数据
        while(pA) 
        {
            sA.emplace(pA), pA = pA ->next;
        }
        while(pB) 
        {
            sB.emplace(pB), pB = pB ->next;
        }
        //弹出
        ListNode * pRes = nullptr;
        while(!sA.empty() && !sB.empty() && sA.top() == sB.top())
        {
            pRes = sA.top();
            sA.pop();
            sB.pop();
        }
        return pRes;
    }
};
#endif
```



正解：

```c++
class Solution {
public:
    ListNode *findFirstCommonNode(ListNode *headA, ListNode *headB) {
        if(!headA || !headB) return nullptr;
        //a->null->b->null  b->null->a->null  期间判断相同
        auto pa = headA, pb = headB;
        while(pa != pb)
        {
            if(pa) pa = pa->next;
            else pa = headB;
            if(pb) pb = pb->next;
            else pb = headA;
        }
        return pa;
    }
};
```



