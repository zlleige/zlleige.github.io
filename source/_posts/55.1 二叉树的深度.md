---
title: 剑指offer——55.1 二叉树的深度
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 55.1 二叉树的深度

[NowCoder](https://www.nowcoder.com/practice/435fb86331474282a3499955f0a41e8b?tpId=13&tqId=11191&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/ba355101-4a93-4c71-94fb-1da83639727b.jpg" width="350px"/> </div><br>

## 解题思路

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
class Solution {
public:
//前序遍历 递归 
    int treeDepth(TreeNode* root) {
        if(!root) return 0;
        
        // int left = treeDepth(root->left);
        // int right = treeDepth(root->right);
        
        // return left >= right ? left + 1 : right + 1;
        return max(treeDepth(root->left) + 1,treeDepth(root->right) + 1) ;
    }
};
```





