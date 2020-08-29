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

# 33. 二叉搜索树的后序遍历序列

[NowCoder](https://www.nowcoder.com/practice/a861533d45854474ac791d90e447bafd?tpId=13&tqId=11176&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。假设输入的数组的任意两个数字都互不相同。

例如，下图是后序遍历序列 1,3,2 所对应的二叉搜索树。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/13454fa1-23a8-4578-9663-2b13a6af564a.jpg" width="150"/> </div><br>

## 解题思路

```java
/**
 * //二叉搜索树特点
对于一棵二叉搜索树，如果不为空，它应该满足以下三个特点：
    1、树上的任一结点，该结点的值都大于它的非空左子树的值。
    2、树上的任一结点，该结点的值都小于它的非空右子树的值。
    3、任一结点的左右子树都是二叉搜索树。

对于二叉搜索树的查找，思路方法是：
1、从根结点开始查找，如果树为空，就返回NULL。
2、如果树不空，就让数据X和根结点的数据Data作比较。
3、如果X的值大于根结点的Data，就往右子树中进行搜索；如果X的值小于根结点的Data，就往左子树中进行搜索。
4、如果X的值等于Data，就表示查找完成，返回该结点。

 * //后续遍历  左右根
输入：[4, 8, 6, 12, 16, 14, 10]
1、根：                  10
2、左子树：最字节的比根小 右子节点比根大 扫前面序列第一个大于根的值，否则不是false
   [4,8,6] 根： 6   [12,16,14] 根：14
             [4] [8]           [12]     [16]  
   
对比到18提
*/

class Solution {
public:
    bool verifySequenceOfBST(vector<int> sequence) {
        if(sequence.empty()) return true;
        return dfs(sequence, 0, sequence.size() - 1);
    }
    
    bool dfs(vector<int>& seq, int l, int r)
    {
        if(l >= r) return true; //边界条件
        int root = seq[r]; //获得根
        int k = l; //用于查找左右子树的分界
        //循环找到左右子树 [1,r- 1]
        while(k < r && seq[k] < root) k ++;
        //检查右子树是否匹配 右边节点比root 小
        for(int i = k; i < r; i ++ )
        {
            if(root >= seq[i]) return false;
        }
        //递归查找左右子树
        return dfs(seq, l, k - 1) && dfs(seq, k, r - 1); 
    }
};



```





