---
title: 剑指offer——46. 把数字翻译成字符串
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 46. 把数字翻译成字符串

[Leetcode](https://leetcode.com/problems/decode-ways/description/)

## 题目描述

给定一个数字，按照如下规则翻译成字符串：1 翻译成“a”，2 翻译成“b”... 26 翻译成“z”。一个数字有多种翻译可能，例如 12258 一共有 5 种，分别是 abbeh，lbeh，aveh，abyh，lyh。实现一个函数，用来计算一个数字有多少种不同的翻译方法。

## 解题思路

```java
/*
动态规划：
1、状态的表示
f[i] 表示第i个字符之前的翻译方法
2、状态如何计算
f[i] = f[i - 1](选择s[i]为单独) + f[i - 2](选择s[i-2]s[i-1]为单独，s[i-2]s[i-1]必须在10-25)
3、边界
f[0] = 1;f[1] = 1; 为了满足f[2] = f[0]+f[1]=>2  "12"=>2种 选2单独ab + 选12单独x 

**/

class Solution {
public:
    int getTranslationCount(string s) {
        if(s.empty()) return 0;
        int len = s.size();
        int f[len + 1] = {0};
        f[0] = 1, f[1] = 1;
        for(int i = 2; i <= len; i ++ )
        {
            f[i] = f[i - 1];
            int tmp = (s[i-2] -'0') * 10 + s[i - 1] - '0';
            //cout << tmp << " "<< (tmp >= 10 && tmp <= 25)<<endl;
            if(tmp >= 10 && tmp <= 25) f[i] += f[i - 2]; 
        }
        return f[len];
     }
};
```






