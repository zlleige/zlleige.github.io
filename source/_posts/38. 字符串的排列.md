---
title: 剑指offer——38. 字符串的排列
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 38. 字符串的排列

[NowCoder](https://www.nowcoder.com/practice/fe6b651b66ae47d7acce78ffdd9a96c7?tpId=13&tqId=11180&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

输入一个字符串，按字典序打印出该字符串中字符的所有排列。例如输入字符串 abc，则打印出由字符 a, b, c 所能排列出来的所有字符串 abc, acb, bac, bca, cab 和 cba。

## 解题思路

```java
class Solution {
public:
    vector<string> Permutation(string str) {
        vector<string> vRec;
        if(str.empty()) return vRec;
        set<string> s;
        Permutation(str, 0, s);
        vRec.assign(s.begin(), s.end());
        return vRec;
    }
     
    /*
    思路：
    递归组合，分别用各个字符的开头，然后一次交换下去，组合所有的情况
    结束条件 交换到最后 bIndex = str.size()
    **/
    void Permutation(string& str, int sIndex, set<string>& vStr)
    {
        // 结束条件 交换到最后 sIndex = str.size()
        if(sIndex >= str.size())
        {
            vStr.emplace(str);
        }
        //循环递归字符串 位置 每次从str开始的sindex开始 (交换每一个用作开头)
        for(int i = sIndex; i < str.size(); i ++)
        {
            swap(str[sIndex], str[i]);
            Permutation(str, sIndex +  1, vStr); //递归下一个节点开头
            swap(str[sIndex], str[i]);
        }
    }
};
```






