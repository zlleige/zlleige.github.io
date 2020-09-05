---
title: 剑指offer——54. 二叉查找树的第 K 个结点
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 54. 二叉查找树的第 K 个结点

[NowCoder](https://www.nowcoder.com/practice/ef068f602dde4d28aab2b210e859150a?tpId=13&tqId=11215&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 解题思路

利用二叉查找树中序遍历有序的特点。

```java
/*
中序遍历；
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
    Solution()
    {
        node = nullptr;
        _k = 0;
    }
    TreeNode* kthNode(TreeNode* root, int k) {
        if(!root) return nullptr;
        _k = k;
        kthNode(root);
        return node;
    }
    
    void kthNode(TreeNode* root)
    {
        if(!root) return;
        if(root->left)  kthNode(root->left, _k);
        _k --;
        if(_k == 0) 
        {
            node = root;
            return;
        }
        if(root->right)  kthNode(root->right, _k);
    }
private:
    int _k;
    TreeNode *node;
    
};
```




