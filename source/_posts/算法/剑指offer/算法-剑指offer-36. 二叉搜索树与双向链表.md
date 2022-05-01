---
title: 剑指offer——36. 二叉搜索树与双向链表
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 36. 二叉搜索树与双向链表

[NowCoder](https://www.nowcoder.com/practice/947f6eb80d944a84850b0538bf0ec3a5?tpId=13&tqId=11179&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/05a08f2e-9914-4a77-92ef-aebeaecf4f66.jpg" width="400"/> </div><br>

## 解题思路

```java
/**
中序遍历：
递归调用：
用一个pair<TreeNode*, TreeNode*> 存左右子树的最左和最右节点，用于最后返回；
每次遍历：举例得到 8 - 10 -12 
根据子树的形态可分为四个情况
1、只有一个节点 当遍历到叶子节点返回 {root,root} 
2、具有左右节点 题设 
   if(!root->left && !root->right)
   {
       //递归获得最后的子树
       //连接最后子树的和根   左子树的有节点-right = root->left， root->right = 右子树的左节点
       返回最后的两个节点
   }
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
    TreeNode* convert(TreeNode* root) {
        //边界
        if(!root) return nullptr;
        auto s = dfs(root);
        return s.first;
    }
    pair<TreeNode*, TreeNode* > dfs(TreeNode* root)
    {
        //叶子节点 返回根
        if(!root->left && !root->right) return {root, root};
        //存在左右节点
        else if(root->left && root->right)
        {
            //递归左右子树
            auto lside = dfs(root->left), rside = dfs(root->right);
            //连接左子树的最后节点-root-右子树的左节点
            auto lnode = lside.second, rnode = rside.first;
            lnode->right = root, root->right = rnode;
            root->left = lnode, rnode->left = root;
            //返回左右子树的最外边节点
            cout <<lnode->val <<" " <<root->val <<" " <<rnode->val  <<endl;
            return {lside.first, rside.second}; 
        }
        //只有左节点
        else  if(root->left)
        {
            //只考虑左子树递归
            auto lside = dfs(root->left);
            //连接 右边不考虑
            auto lnode = lside.second;
            lnode->right = root, root->left = lnode;
            //返回
            //cout <<lnode->val <<" " <<root->val  <<endl;
            return {lside.first, root};
        }
        //只有右边节点
        else 
        {
            //考虑右子树
            auto rside = dfs(root->right);
            //连接
            auto rnode = rside.first;
            rnode->left = root, root->right = rnode;
            //返回
            //cout <<root->val <<" " <<rnode->val  <<endl;
            return make_pair(root,rside.second);
        }
    }
};
```




