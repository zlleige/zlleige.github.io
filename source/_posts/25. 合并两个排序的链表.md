---
title: 剑指offer——25. 合并两个排序的链表
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 25. 合并两个排序的链表

[NowCoder](https://www.nowcoder.com/practice/d8b6b4358f774294a89de2a6ac4d9337?tpId=13&tqId=11169&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/c094d2bc-ec75-444b-af77-d369dfb6b3b4.png" width="400"/> </div><br>

## 解题思路

### 递归

```java
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 
  #if 1 //迭代实现
class Solution {
public:
    ListNode* merge(ListNode* l1, ListNode* l2) {
        //边界 z保证以下都合法
        if(!l1) return l2;
        if(!l2) return l1;
        //创建一个用于返回的节点
        ListNode* conn = new ListNode(0);
        ListNode*  tmp = conn; //跟踪
        ListNode* p1 = l1, *p2 = l2; //跟踪
        
        while(p1 && p2)  //公共区域
        {
             if(p1->val < p2->val)
            {
                tmp->next = p1;
                p1 = p1->next; 
            }
            else
            {
                 tmp->next = p2;
                p2 = p2->next;
            }
            tmp = tmp->next;
        }
        
        tmp->next = (p1) ? p1 : p2; 
        return conn->next;
    }  
};
#endif
```

### 迭代

```java
class Solution {
public:
    ListNode* merge(ListNode* l1, ListNode* l2) {
        //边界 z保证以下都合法
        if(!l1) return l2;
        if(!l2) return l1;
        ListNode* conn = nullptr;
        if(l1->val < l2->val)
        {
            conn = l1;
            conn->next = merge(l1->next, l2);
        }
        else
        {
            conn = l2;
            conn->next = merge(l1, l2->next);
        }
        return conn;
    }  
};
```



