---
title: 剑指offer——24. 反转链表
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 24. 反转链表

[NowCoder](https://www.nowcoder.com/practice/75e878df47f24fdc9dc3e400ec6058ca?tpId=13&tqId=11168&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 解题思路

### 递归

```java
/**
递归方案
https://blog.csdn.net/fx677588/article/details/72357389
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
    ListNode* reverseList(ListNode* head) {
        //边界
        if(!head || !head->next) return head;
        //递归到倒数第二个节点 head为倒数第二个节点
        ListNode* p = reverseList(head->next); //head->next = nullptr时返回 
        head->next->next = head;
        head->next = nullptr;
        return p ; 
    }
};
```

### 迭代

使用头插法。

```java
/*
思路：
交换节点：
定义节点  
pCurr = head:用于遍历 
pPre = nullptr :保存前一个节点
pNext: 实时更新pCurr的下一个节点

交换：
whlie(pCurr)
{
    ListNode* pNext = pCurr->next;
    pCurr->next = pPre; //当前指向前一个
    pPre = pCurr;
    pCurr = pNext;
}

**/

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
    ListNode* reverseList(ListNode* head) {
        if(!head || !head->next) return head;
        ListNode *pCurr  = head;
        ListNode *pPre = nullptr;
        ListNode *pNext = nullptr;
        while(pCurr)
        {
            pNext = pCurr->next;
            pCurr->next = pPre;
            pPre = pCurr;
            pCurr = pNext;
        }
        return pPre;
    }
};

```





