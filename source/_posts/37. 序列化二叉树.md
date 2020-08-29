---
title: 剑指offer——37. 序列化二叉树
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 37. 序列化二叉树

[NowCoder](https://www.nowcoder.com/practice/cf7e25aa97c04cc1a68c8f040e71fb84?tpId=13&tqId=11214&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

请实现两个函数，分别用来序列化和反序列化二叉树。

## 解题思路

```java
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 * 思路：
 * 可以通过前序中序后续层序等遍历方式
 * 确保打包和解析的方式相同
 */
class Solution {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        string str = "";
        pre_serialize(root, str);
        //cout << str;
        return str;
    }
    
    void pre_serialize(TreeNode* root, string & str) {
        if(!root) 
        {
            str += string("null") + " ";
            return;
        }
        str += std::to_string(root->val) + " ";
        pre_serialize(root->left, str);
        pre_serialize(root->right, str);
    }
    
    #if 0//空间复杂度 On
    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        
        vector<string> vStr; //用于分割string
        string strTmp;
        stringstream input(data);
        while(getline(input,strTmp,' '))
            vStr.emplace_back(strTmp);
        
        // cout << vStr.size()<< endl;
        // for(auto& x : vStr)
        // {
        //     cout << x << " "; 
        // }
        // cout <<endl;
        int index = 0;
        return dfs_d(vStr, index);
    }
    
    //解析数据 主要是分割字符串处理
    TreeNode* dfs_d(vector<string>& vStr, int &index)
    {
        if(index == vStr.size()) return nullptr;
        if(vStr[index].at(0) == 'n') 
        {
            index ++;
            return nullptr;
        }
       
        auto root = new TreeNode(stoi(vStr[index ++]));
        root->left = dfs_d(vStr, index );
        root->right = dfs_d(vStr, index );
        return root;
    }
    #endif
    
    #if 1 // O1的空间复杂度
     // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        int index = 0;
        return dfs1_d(data, index);
    }
    
    TreeNode* dfs1_d(string& str, int& index)
    {
        if(index == str.size()) return nullptr;
        int k = index; //用一个变量记录当前分割
        while(str[k] != ' ') k++;  //量出一个节点数据 
        if(str[index] == 'n')  //如果当前数据为null 更新位置后返回
        {
            index = k + 1; 
            return nullptr;
        }
        //string( string &str, size_type index, size_type length );
        string val(str, index, k - index);
        index = k + 1;
        auto root = new TreeNode(stoi(val));
        root->left = dfs1_d(str, index);
        root->right = dfs1_d(str, index);
        return root;
    }
    #endif
};

```





