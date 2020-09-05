---
title: 剑指offer——50. 第一个只出现一次的字符位置
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 50. 第一个只出现一次的字符位置

[NowCoder](https://www.nowcoder.com/practice/1c82e8cf713b4bbeb2a5b31cf5b0417c?tpId=13&tqId=11187&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

在一个字符串中找到第一个只出现一次的字符，并返回它的位置。

```
Input: abacc
Output: b
```

## 解题思路

```c++
/*
思路： O(2n)
用一个unordered_map遍历string，键值对《char, int count出现个数》; 
遍历哈希，找到第一个值为一的数据
**/
class Solution {
public:
    char firstNotRepeatingChar(string s) {
        char res = '#';
        if(s.empty()) return  res;
        unordered_map<char, int> dat;
        for(auto x : s)
        {
            dat[x] ++; //不能break；后面的数据有可能也重复  必须轮询完
        }
        for(auto x : s)
        {
            if(dat[x] == 1) 
            {
                res = x;
                break;
            }
        }
        return res;
    }
};
```




