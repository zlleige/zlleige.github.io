---
title: 剑指offer——32.1 从上往下打印二叉树
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 32.1 从上往下打印二叉树

[NowCoder](https://www.nowcoder.com/practice/7fe2212963db4790b57431d9ed259701?tpId=13&tqId=11175&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

从上往下打印出二叉树的每个节点，同层节点从左至右打印。

例如，以下二叉树层次遍历的结果为：1,2,3,4,5,6,7

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/d5e838cf-d8a2-49af-90df-1b2a714ee676.jpg" width="250"/> </div><br>

## 解题思路

使用队列来进行层次遍历。

不需要使用两个队列分别存储当前层的节点和下一层的节点，因为在开始遍历一层的节点时，当前队列中的节点数就是当前层的节点数，只要控制遍历这么多节点数，就能保证这次遍历的都是当前层的节点。

```java
/****层序遍历
设计一个queue 
front 指针指向root
1、先加入front

2、循环整个queue
  1）加入front的左右节点
  2）弹出对头
*/

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> printFromTopToBottom(TreeNode* root) {
        vector<int> vec;
        if(!root) return vec;
        queue<TreeNode*> que;
        TreeNode* front = nullptr;
        que.push(root);
        
        while(!que.empty())
        {
            //加入左右节点
            front = que.front();
            vec.push_back(que.front()->val);
            if(front->left) que.push(front->left);
            if(front->right) que.push(front->right);
            
            //弹出队头
            que.pop();
        }
        return vec;
    }
};
```






