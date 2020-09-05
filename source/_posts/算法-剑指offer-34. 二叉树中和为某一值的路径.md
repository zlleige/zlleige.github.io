---
title: 剑指offer——33. 二叉搜索树的后序遍历序列
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 34. 二叉树中和为某一值的路径

[NowCoder](https://www.nowcoder.com/practice/b736e784e3e34731af99065031301bca?tpId=13&tqId=11177&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

输入一颗二叉树和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。

下图的二叉树有两条和为 22 的路径：10, 5, 7 和 10, 12

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/ed77b0e6-38d9-4a34-844f-724f3ffa2c12.jpg" width="200"/> </div><br>

## 解题思路

```java
/*
深度优先遍历：推演过程： 前序遍历 根 左 右边
num=22。
      5
     / \
    4   6
   /   / \
  12  13  6
 /  \    / \
9    1  5   1
首先：
1、第一个dfs(root->left, sum, vRes,vPatn); 
：先遍历左分支 5，4，12，9  root->12 sum余下 22-(5+4+12+9) = -8 return
**/
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
    vector<vector<int>> findPath(TreeNode* root, int sum) {
        vector<vector<int>> vRes;
        vector<int> vPatn;
        dfs(root, sum, vRes,vPatn);
        return vRes;
    }
    
    void dfs(TreeNode* root, int sum, vector<vector<int>> &vRes,vector<int>& vPatn)
    {
        //结束条件  当前分支为空 并且sum的值已经不足 没必要继续向下分支继续
        if(!root || sum <= 0 ) return;
        //加入数据
        vPatn.emplace_back(root->val);
        sum -= root->val; //sum的每一个值都有记录
        //恰好匹配 当前为叶子节点并且sum=0
        if(!root->left && !root->right && sum == 0) 
        {
            vRes.emplace_back(vPatn); 
        }
        dfs(root->left, sum, vRes,vPatn);
        dfs(root->right, sum, vRes,vPatn);
        vPatn.pop_back(); //删掉最后一个元数 回到前序遍历的上一个节点
    }
};

```





