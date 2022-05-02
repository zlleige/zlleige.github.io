---
title: 剑指offer——6. 从尾到头打印链表
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 6. 从尾到头打印链表

## 题目链接

[牛客网](https://www.nowcoder.com/practice/d0267f7f55b3412ba93bd35cfa8e8035?tpId=13&tqId=11156&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

从尾到头反过来打印出每个结点的值。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/f5792051-d9b2-4ca4-a234-a4a2de3d5a57.png" width="300px"> </div><br>

## 解题思路

### 1. 使用递归

要逆序打印链表 1->2->3（3,2,1)，可以先逆序打印链表 2->3(3,2)，最后再打印第一个节点 1。而链表 2->3 可以看成一个新的链表，要逆序打印该链表可以继续使用求解函数，也就是在求解函数中调用自己，这就是递归函数。

```c++
class Solution {
public:
    vector<int> data;
    vector<int> printListFromTailToHead(ListNode* head) {
       if(head != NULL)
       {
           printListFromTailToHead(head->next);
           data.emplace_back(head->val);
       }
        return data;
    }
};
```

### 2. 使用头插法

头插法顾名思义是将节点插入到头部：在遍历原始链表时，将当前节点插入新链表的头部，使其成为第一个节点。

链表的操作需要维护后继关系，例如在某个节点 node1 之后插入一个节点 node2，我们可以通过修改后继关系来实现：

```java
node3 = node1.next;
node2.next = node3;
node1.next = node2;
```

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/58c8e370-3bec-4c2b-bf17-c8d34345dd17.gif" width="220px"> </div><br>



为了能将一个节点插入头部，我们引入了一个叫头结点的辅助节点，该节点不存储值，只是为了方便进行插入操作。不要将头结点与第一个节点混起来，第一个节点是链表中第一个真正存储值的节点。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/0dae7e93-cfd1-4bd3-97e8-325b032b716f-1572687622947.gif" width="420px"> </div><br>

```java
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* pPre = nullptr;
        ListNode* pCurr = head;
        while(pCurr)
        {
            ListNode* pNext = pCurr->next; //记录当前节点的下一个节点
            pCurr->next = pPre; //当前节点指向前一个节点
            pPre = pCurr; //前一个节点指向当前
            pCurr = pNext;
        } 
        return pPre; //为什么 因为到左后一个节点的时候  pPre正好等于最后一个节点
    }
};
```

### 3. 使用栈

栈具有后进先出的特点，在遍历链表时将值按顺序放入栈中，最后出栈的顺序即为逆序。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/9d1deeba-4ae1-41dc-98f4-47d85b9831bc.gif" width="340px"> </div><br>

```java
class Solution {
public:
    ListNode* ReverseList(ListNode* pHead) {
        if(!pHead || !pHead->next) return pHead;
        ListNode* pList = pHead;
        stack<int> tmp;
        while(pList)
        {
            tmp.push(pList->val);
            pList = pList->next;
        }
        pList = pHead;
        while(pList)
        {
            pList->val = tmp.top();
            pList = pList->next;
            tmp.pop();
        }
        return pHead;
    }
};
```



### java实现



#### 1 使用栈

空间复杂度O(N), 时间复杂度O(N)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public int[] reversePrint(ListNode head) {
        if(head == null) return new int[]{};
        Stack<Integer> stack = new Stack();
        ListNode curr = head;
        while(curr != null) {
            stack.push(curr.val);
            curr = curr.next;
        }
        int[] res = new int[stack.size()];
        int i = 0;
        while(!stack.empty()) {
            res[i++] = stack.pop();
        }
        return res;
    }
}
```



#### 2 直接使用数组返回

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public int[] reversePrint(ListNode head) {
        // 时间复杂度O(2N) 空间复制度O(N)
        if(head == null) return new int[]{};
        ListNode curr = head;
        // 获取链表长度
        int nodeLen  = 0;
        while(curr != null) {
          nodeLen ++;
          curr = curr.next;
        }

        curr = head;
        // 初始化返回数组，再遍历链表
        int[] res = new int[nodeLen];
        int i = nodeLen - 1;
        while(curr != null) {
          res[i --] = curr.val;
           curr = curr.next;
        }
        return res;
    }
}
```

