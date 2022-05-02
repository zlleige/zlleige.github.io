---
title: 剑指offer——7. 重建二叉树
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 7. 重建二叉树

## 题目链接

[牛客网](https://www.nowcoder.com/practice/8a19cbe657394eeaac2f6ea9b0f6fcf6?tpId=13&tqId=11157&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

根据二叉树的前序遍历和中序遍历的结果，重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。



<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/image-20191102210342488.png" width="400"/> </div><br>

## 解题思路

前序遍历的第一个值为根节点的值，使用这个值将中序遍历结果分成两部分，左部分为树的左子树中序遍历结果，右部分为树的右子树中序遍历的结果。然后分别对左右子树递归地求解。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/60c4a44c-7829-4242-b3a1-26c3b513aaf0.gif" width="430px"> </div><br>

```java
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

    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        map<int, int> vHash;
        for(int i = 0; i < inorder.size(); i ++)
        {
            vHash[inorder[i]] = i;
        }
        return dfs(preorder,0,preorder.size() - 1, vHash, 0, inorder.size() - 1);
    }
    
    /*
    说明：
    vector<int> vPre; //用于存前序遍历结果 
    pl：前序的起点
    pr：前序的终点
    il：中序的起点
    ir：中序的终点
    map<vector<int>> vHash; //用于存入中序的结果，更容易获得中序元素的位置
    */
    TreeNode* dfs(vector<int>& preorder, int pl, int pr, map<int, int>& vHash, int il,int ir)
    {  
        if(pl > pr) return nullptr;
        TreeNode* root = new TreeNode(preorder[pl]); //根为前序的第一个节点
        int k = vHash[root->val]; //找到对应中序中的根节点位置
        root->left = dfs(preorder,pl + 1, pl + k - il, vHash,il, k - 1 ); //获得前序遍历左子树 
        root->right = dfs(preorder,pl + k -il + 1, pr, vHash,k + 1, ir );
        return root;
    }
};
```



**拓展：**

已知中序和前序、中序和后序可以推出整个二叉树

实现后续和中序的操作：

```c++
//--主要考虑递归实时位置的确定
//前序：根 +左子树 +右子树
//后续：最后一个为根，考虑为前序的逆过程  结构：左子树+右子树+根
//中序结构： 左子树 + 根 +右子树
 //--过程
 1、创建节点 root -》后续的最后一个值
 2、找到中序k位置，k-il = 左子树个数 
 3、添加左子树部分：
    后序位置：(pl, pl + k - il)  //结构：左子树+右子树+根
    中序位置：(il, k - 1)  //结构：左子树 + 根 +右子树
4、添加右子树部分：
后序位置：(pl + k - il + 1, pr - 1)  //结构：左子树+右子树+根
中序位置：(k + 1, ir)  //结构：左子树 + 根 +右子树

TreeNode* dfs(vector<int>& postorder, int pl, int pr, map<int, int>& vHash, int il,int ir)
{  
    if(pl > pr) return nullptr;
    TreeNode* root = new TreeNode(preorder[pr]); //根为前序的最后节点
    int k = vHash[root->val]; //找到对应中序中的根节点位置
    root->left = dfs(postorder,pl, pl + k - il, vHash,il, k - 1 ); //获得前序遍历左子树 
    root->right = dfs(postorder,pl + k -il + 1, pr - 1, vHash,k + 1, ir );
    return root;
}

```



#### java 实现

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    // 前序遍历： 根 左 右,前序遍历的第一个点即使根
    // 中序遍历： 左 根 右


    public TreeNode buildTree(int[] pre, int[] in) {
        if(pre.length==0 || in.length == 0) return null;
        Map<Integer, Integer> inMap = new HashMap<>();
        for(int i = 0; i < in.length; i ++) {
            inMap.put(in[i], i);
        }
        return buildTree(pre, 0, pre.length-1, inMap, 0, in.length-1);
    }

    TreeNode buildTree(int[] pre, int pl, int pr, Map<Integer, Integer> inMap, int il, int ir) {
        if(pl > pr || il > ir) {
            return null;
        } 
        // preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
        // 前序遍历preorder的第一点即为根3
        TreeNode node = new TreeNode(pre[pl]);
        // 找到中序遍历中根的位置 pos = 1
        int pos = inMap.get(pre[pl]);
        // 构建左子树 preorder = [9], inorder = [9]
        node.left = buildTree(pre, pl + 1, pl +  (pos - il), inMap, il , pos - 1);
        // 构建右子树 preorder = [20,15,7], inorder = [15,20,7]
        node.right = buildTree(pre,  pl +  (pos - il) +1, pr, inMap, pos +1, ir);
        return node;
    }


}
```



