---
title: 剑指offer——23. 链表中环的入口结点
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 23. 链表中环的入口结点

[acwing](https://www.acwing.com/solution/acwing/content/741/)

## 题目描述

一个链表中包含环，请找出该链表的环的入口结点。要求不能使用额外的空间。

## 解题思路

使用双指针，一个快指针 fast 每次移动两个节点，一个慢指针 slow 每次移动一个节点。因为存在环，所以两个指针必定相遇在环中的某个节点上。

假设环入口节点为 y1，相遇所在节点为 z1。

假设快指针  fast  在圈内绕了 N 圈，则总路径长度为 x+Ny+(N-1)z。z 为 (N-1) 倍是因为快慢指针最后已经在 z1 节点相遇了，后面就不需要再走了。

而慢指针 slow 总路径长度为 x+y。



我们要找的是环入口节点 y1，也可以看成寻找长度 x 的值，因此我们先将上面的等值分解为和 x 有关：x=(N-2)y+(N-1)z。

上面的等值没有很强的规律，但是我们可以发现 y+z 就是圆环的总长度，因此我们将上面的等式再分解：x=(N-2)(y+z)+z。这个等式左边是从起点x1 到环入口节点 y1 的长度，而右边是在圆环中走过 (N-2) 圈，再从相遇点 z1 再走过长度为 z 的长度。此时我们可以发现如果让两个指针同时从起点 x1 和相遇点 z1 开始，每次只走过一个距离，那么最后他们会在环入口节点相遇。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/bb7fc182-98c2-4860-8ea3-630e27a5f29f.png" width="500"/> </div><br>

```java
/**
 思路：
 1、定义快慢两个指针 ：ps pf  步进分别：1 2
 2、找到相遇的点
 3、慢指针从头，快指针从当前位置  同时 步进1 直到相遇
 
 4、空环
 [1]
  0
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
    ListNode *entryNodeOfLoop(ListNode *head) {
       if(!head || !head->next) return nullptr;
       ListNode* ps = head;
       ListNode* pl = head;
       
       while(pl && pl->next)
       {
           ps = ps->next;
           pl = pl->next->next;
           if(ps == pl) break;
       }
       //判断是否有环 !pl->next：防止单节点输入
       if(ps != pl || !pl->next) return nullptr;
       //单环
       if(pl == pl->next) return pl;
       ps = head;
       while(ps != pl)
       {
           ps = ps->next;
           pl = pl->next;
       }
       return ps;
    }
};
```





