---
title: 剑指offer——8. 二叉树的下一个结点
date: 2020-02-15   
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 8. 二叉树的下一个结点

## 题目链接

[牛客网](https://www.nowcoder.com/practice/9023a0c988684a53960365b889ceaf5e?tpId=13&tqId=11210&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

给定一个二叉树和其中的一个结点，请找出中序遍历顺序的下一个结点并且返回 。注意，树中的结点不仅包含左右子结点，同时包含指向父结点的指针。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode *father;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL), father(NULL) {}
 * };
 */
```

## 解题思路

我们先来回顾一下中序遍历的过程：先遍历树的左子树，再遍历根节点，最后再遍历右子树。所以最左节点是中序遍历的第一个节点。

① 如果一个节点的右子树不为空，那么该节点的下一个节点是右子树的最左节点；

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/7008dc2b-6f13-4174-a516-28b2d75b0152.gif" width="300px"/> </div><br>

② 否则，向上找第一个左链接指向的树包含该节点的祖先节点。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/094e3ac8-e080-4e94-9f0a-64c25abc695e.gif" width="300px"/> </div><br>

```c++
 //我的代码，考虑三种情况
 /*
  //1--存在右子树 找最有一个左节点即为后续
  //2--不存在右子树，节点为左子节点 后继为父节点
  //3--不存在右子树，节点为右子节点 后继为向上遍历到一个节点为其父节点的字节点，这个节点的父节点即为后记
   //23可以兼容：考虑当前节点无右子树，判断当前节点的father是否存在 && 当前节点是否为左节点，左节点的father即为后记     
 */
class Solution {
public:
    TreeNode* inorderSuccessor(TreeNode* p) {
        if(!p) return nullptr;
        //--存在右子树 找最有一个左节点即为后续
        if(p->right)
        {
            p = p->right;
            while(p->left)
            {
                p = p->left;
            }
            return p;
        }
        //--不存在右子树，节点为左子节点 后继为父节点
        else if(p->father && p ==  p->father->left)
        {
            return p->father;
        }
        //--不存在右子树，节点为右子节点 后继为向上遍历到一个节点为其父节点的字节点，这个节点的父节点即为后记
        else //if(p->father && p == p->father->right)  //特殊情况 一个根节点过来，满足情况
        {
            while(p->father && p == p->father->right) p = p->father; //直到找到左节点
            return p->father;
        }
        
    }
};

//改良后的程序
//兼容了左节点情况
class Solution {
public:
    TreeNode* inorderSuccessor(TreeNode* p) {
        if (p->right) {
            p = p->right;
            while (p->left) p = p->left;
            return p;
        }

        while (p->father && p == p->father->right) p = p->father;
        return p->father;
    }
};
```





