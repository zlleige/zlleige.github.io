---
title: 剑指offer——28. 对称的二叉树
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 28. 对称的二叉树

[NowCoder](https://www.nowcoder.com/practice/ff05d44dfdb04e1d83bdbdab320efbcb?tpId=13&tqId=11211&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/0c12221f-729e-4c22-b0ba-0dfc909f8adf.jpg" width="300"/> </div><br>

## 解题思路

```java
/**
思路1：递归
-镜像
--1 根节点相同 
--2 左右子树镜像
    根的左子节点=根的右子节点
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
    bool isSymmetric(TreeNode* root) {
        //边界
        if(!root) return true; //空树对称
        return Symmetric(root->left, root->right);
    }
    
    //判断左右是否镜像
    bool Symmetric(TreeNode* left,TreeNode* right)
    {
        //边界条件 找到最后了 判断如果时left和right均为空 则匹配完成
        if(!left || !right) return !left && !right;
        //判断规则  值相同 递归 左子树的左==右子树的右 和 左子树的右==右子树的左 镜像
        return left->val == right->val && Symmetric(left->left, right->right) &&  Symmetric(left->right, right->left);
        // if(left->val == right->val)
        // {
        //     return Symmetric(left->left, right->right) &&  Symmetric(left->right, right->left);
        // }
        // else return false;
    }
};
```






