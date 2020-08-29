---
title: 剑指offer——32.2 把二叉树打印成多行
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 32.2 把二叉树打印成多行

[NowCoder](https://www.nowcoder.com/practice/445c44d982d04483b04a54f298796288?tpId=13&tqId=11213&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

和上题几乎一样。

## 解题思路

```java
/*
基于层序遍历
一个队列依次装入节点
设置两个变量  
一个用于记录当前层的数量currNum 初始为1：表示当前加入了根节点：每次装载数据后-- 为零时更新 currNum = nextNum; nextNum = 0;
一个用于记录下一层的数量nextNum：判断每一次数据的左右节点时 存在则++
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
    vector<vector<int>> printFromTopToBottom(TreeNode* root) {
       vector<vector<int>> vRes;
       if(!root) return vRes;
       vector<int> vTmp; //暂存每一层数据
       
       queue<TreeNode*> que; //BFS
       que.push(root);
       int currNum = 1, nextNum = 0;
       while(!que.empty())
       {
           auto top = que.front(); //记录对头
           que.pop(); //出对
           //左右节点 入队列
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
          //加入打印数据 同时当前层数据数-1
          vTmp.push_back(top->val);
          currNum --;
          if(currNum <= 0)
          {
              currNum = nextNum;
              vRes.emplace_back(vTmp);
              vTmp.clear();
              nextNum = 0;
          }
       }
       return vRes;
    }
};
```





