---
title: 剑指offer——18.2 删除链表中重复的结点
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 18.2 删除链表中重复的结点

[NowCoder](https://www.nowcoder.com/practice/fc533c45b73a41b0b44ccba763f866ef?tpId=13&tqId=11209&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/17e301df-52e8-4886-b593-841a16d13e44.png" width="450"/> </div><br>

## 解题描述

```java
//思路用一个map 存值和链表地址  实现每次加入时只取重复元素的一个
//set记录当前重复的值，当判断存在相同点，即删除

/*
set 的insert 和 emplace
必须明确一个概念就是，容器中插入的元素永远都不是元素本身，而是元素的一份copy。emplace其实就是调用了拷贝构造函数，在容器创建元素时，就直接根据需要插入的元素进行了构造。而insert,push_back等，先是构造了元素，在调用了重载运算符函数，对函数进行了赋值。所以比较耗时。故推荐使用emplace组的函数进行插入。
emplace族的三个函数：emplace_front(),emplace_back(),emplace()
--------------------- 
作者：不然秋月春风夜 
来源：CSDN 
原文：https://blog.csdn.net/m0_38126105/article/details/85042807 
版权声明：本文为博主原创文章，转载请附上博文链接！

set<int> s;
	pair<set<int>::iterator,bool> ret = s.insert(10);
	if (ret.second){
		cout << "插入成功:" << *ret.first << endl;
	}
	else{
		cout << "插入失败:" << *ret.first << endl;
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
    ListNode* deleteDuplication(ListNode* head) {
        if(!head ) return nullptr;
        //map 键：val  值：指针  
        map<int, ListNode*> tmp;
        set<ListNode*> dealNodes;
        ListNode* pNode = head;
        while(pNode)
        {
            int val = pNode->val;
            if(!tmp.emplace(val, pNode).second)
            {
                deleteNode(pNode);
                dealNodes.emplace(tmp[val]);
                //deleteNode(tmp[val]);
                //tmp.erase(val);
            }
            else  pNode = pNode->next;
        }
        
        
        for(auto it = dealNodes.begin(); it != dealNodes.end(); it ++)
            cout << (*it)->val ;
            //deleteNode(*it);
         cout <<endl;
       return head;
    }
    
    //删除当前节点  参考上一个提
    void deleteNode(ListNode* node)
    {
        auto p = node->next;
        node->val = p->val;
        node->next = p->next;
        // 这两步的作用就是将 *(node->next) 赋值给 *node，所以可以合并成一条语句：
        // *node = *(node->next);
        delete p;
    }
};
```







