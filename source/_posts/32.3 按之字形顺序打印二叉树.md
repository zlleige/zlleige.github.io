---
title: 剑指offer——32.3 按之字形顺序打印二叉树
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 32.3 按之字形顺序打印二叉树

[NowCoder](https://www.nowcoder.com/practice/91b69814117f4e8097390d107d2efbe0?tpId=13&tqId=11212&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

请实现一个函数按照之字形打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右至左的顺序打印，第三行按照从左到右的顺序打印，其他行以此类推。

## 解题思路

```java
/*
思路：基于层序遍历
1、设置两个变量，
    一个记录当前层的数据个数currNum：初始化为1 每次弹出数据都-1
    一个记录下一层的数据nextNum：判断当前层有左右节点 ++
    当currNum = 0时,换层 操作：currNum = nextNum; nextNum = 0; 装入层数据


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
    vector<vector<int>> printFromTopToBottom(TreeNode* root) {
        vector<vector<int>> vRes;
        if(!root) return vRes;
        vector<int> vTmp;
        int currNum = 1, nextNum = 0;
        queue<TreeNode *> que;
        que.push(root);
        bool isReserve = false; //定义标志是否要反转vector
        while(!que.empty())
        {
            auto top = que.front();
            que.pop();
            if(top->left)
            {
                que.push(top->left);
                nextNum ++;
            }
            if(top->right)
            {
                que.push(top->right);
                nextNum ++;
            }
            //加入数据
            vTmp.emplace_back(top->val);
            currNum --;
            if(currNum <= 0)
            {
                //currNum = nextNum;
                //nextNum = 0;
                //if(isReserve) std::reverse(vTmp.begin(), vTmp.end()); //反转数据
                //isReserve = !isReserve; //反转标志
                //vRes.emplace_back(vTmp);
                //vTmp.clear();
                
                currNum = nextNum;
                nextNum = 0;
                if(isReserve)  vRes.emplace_back(vector<int>(vTmp.rbegin(), vTmp.rend())); //用匿名对象 构造函数传cTmp的反相
                else vRes.emplace_back(vTmp);
                isReserve = !isReserve; //反转标志
                vTmp.clear();
            }
        }
        return vRes;
    }
};
```





