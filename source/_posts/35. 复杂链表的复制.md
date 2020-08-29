---
title: 剑指offer——35. 复杂链表的复制
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 35. 复杂链表的复制

[NowCoder](https://www.nowcoder.com/practice/f836b2c43afc4b35ad6adc41ec941dba?tpId=13&tqId=11178&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针指向任意一个节点），返回结果为复制后复杂链表的 head。

```java
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
```

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/66a01953-5303-43b1-8646-0c77b825e980.png" width="300"/> </div><br>

## 解题思路

第一步，在每个节点的后面插入复制的节点。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/dfd5d3f8-673c-486b-8ecf-d2082107b67b.png" width="600"/> </div><br>

第二步，对复制节点的 random 链接进行赋值。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/cafbfeb8-7dfe-4c0a-a3c9-750eeb824068.png" width="600"/> </div><br>

第三步，拆分。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/e151b5df-5390-4365-b66e-b130cd253c12.png" width="600"/> </div><br>

```java
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
        if(!pHead) return NULL;
        RandomListNode *cur = pHead;
        while(cur){
            RandomListNode *node = new RandomListNode(cur->label);
            node->next = cur->next;
            cur->next = node;
            cur = node->next;
        }//直到cur指向了原先链表的结尾null处
        cur = pHead;
        RandomListNode *p;
        while(cur){
             p = cur->next;
            if(cur->random){
                p->random = cur->random->next;
                  
            }
            cur = p->next;
        }
          
        RandomListNode *pCloneHead = pHead->next;
        RandomListNode *tmp;
        cur = pHead;
        while(cur->next){
            tmp = cur->next;
            cur->next =tmp->next;
            cur = tmp;
        }
        return pCloneHead;
    }
};
```





