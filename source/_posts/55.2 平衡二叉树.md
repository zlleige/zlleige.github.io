---
title: 剑指offer——55.2 平衡二叉树
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 55.2 平衡二叉树

[NowCoder](https://www.nowcoder.com/practice/8b3b95850edb4115918ecebdf1b4d222?tpId=13&tqId=11192&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

平衡二叉树左右子树高度差不超过 1。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/af1d1166-63af-47b6-9aa3-2bf2bd37bd03.jpg" width="250px"/> </div><br>

## 解题思路

```java
/*
（1）非叶子节点最多拥有两个子节点；
（2）非叶子节值大于左边子节点、小于右边子节点；
（3）树的左右两边的层级数相差不会大于1;
（4）没有值相等重复的节点;

***/

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
    bool isBalanced(TreeNode* root) {
        if(!root) return true;
        int high = getHight(root);
        return high >= 0;
    }
    
    //求平衡二叉树的深度 如果不是平衡二叉树 直接返回-1
    int getHight(TreeNode* root)
    {
        if(!root) return 0;
        int left = getHight(root->left);
        if(left < 0) return -1;
        int right = getHight(root->right);
        if(right < 0) return -1;
        if(abs(left - right) > 1) return -1;
        else return max(left, right) + 1;
    }
};


/*
求二叉树深度 如果深度相差为1 标志false
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
    bool isBalanced(TreeNode* root) {
        bool isTrue = true;
        getHigh(root, isTrue);
        return isTrue;
    }
    
    int getHigh(TreeNode* root, bool& isTrue)
    {
        if(!root) return 0;
        int left = getHigh(root->left, isTrue) + 1;
        int right = getHigh(root->right, isTrue) + 1;
        if(abs(left - right) > 1) isTrue = false;
        return max(left, right);
    }
};

```





