---
title: 剑指offer——26. 树的子结构
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 26. 树的子结构

[NowCoder](https://www.nowcoder.com/practice/6e196c44c7004d15b1610b9afca8bd88?tpId=13&tqId=11170&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/84a5b15a-86c5-4d8e-9439-d9fd5a4699a1.jpg" width="450"/> </div><br>

## 解题思路

```java
/*
思路： 递归
1、遍历A找到匹配的头
    if(pRoot1->val == pRoot2->val)
    {
        //匹配结构
    }
    
    return hasSubtree(pRoot1->left) || hasSubtree(pRoot1->right); 
2、匹配判断结构是否相等
    bool isSame(TreeNode* p1, TreeNode* p2)
    {
        //边界条件  p2为空  遍历完了 -》true
        if(!p2) return true; 
        if(!p1 || p1->val != p2->val) return false; //p1为空且p2不为空 或者值不匹配 false
        return isSame(p1->left, p2->left) && isSame(p1->right, p2->right)
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
    bool hasSubtree(TreeNode* pRoot1, TreeNode* pRoot2) {
        if(!pRoot1 || !pRoot2) return false;
        if(pRoot1->val == pRoot2->val)
        {
            //判断当前分支是否匹配
            if( isSame(pRoot1, pRoot2)) return true;
        }
        return hasSubtree(pRoot1->left, pRoot2) || hasSubtree(pRoot1->right, pRoot2); 
    }
    
    bool isSame(TreeNode* p1, TreeNode* p2)
    {
        //边界条件  p2为空  遍历完了 -》true
        if(!p2) return true; 
        if(!p1 || p1->val != p2->val) return false; //p1为空且p2不为空 或者值不匹配 false
        return isSame(p1->left, p2->left) && isSame(p1->right, p2->right);
    }
};
```





