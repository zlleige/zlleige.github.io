---
title: 剑指offer——22. 链表中倒数第 K 个结点
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 22. 链表中倒数第 K 个结点

[NowCoder](https://www.nowcoder.com/practice/529d3ae5a407492994ad2a246518148a?tpId=13&tqId=11167&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 解题思路

设链表的长度为 N。设置两个指针 P1 和 P2，先让 P1 移动 K 个节点，则还有 N - K 个节点可以移动。此时让 P1 和 P2 同时移动，可以知道当 P1 移动到链表结尾时，P2 移动到第 N - K 个节点处，该位置就是倒数第 K 个节点。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/6b504f1f-bf76-4aab-a146-a9c7a58c2029.png" width="500"/> </div><br>

```java
/*
思路：
1、一轮遍历  得到链表的长度
2、二轮遍历 得到要找的元素

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
    ListNode* findKthToTail(ListNode* pListHead, int k) {
        int len = 0;
        ListNode* pList = pListHead;
        while(pList) 
        {
           len ++;
           pList = pList->next;
        }
       // cout << len <<endl;
        int num = len - k; //例如链表：1->2->3->4->5 ，k=2 len=5 实际num从0开始 移动len-k=3次 
        if(num < 0) return nullptr;
        pList = pListHead;
        while(num > 0)
        {
            num--;
            pList = pList->next;
        }
        
        return pList;
    }
};
```





