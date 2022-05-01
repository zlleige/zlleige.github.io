---
title: 剑指offer——48. 最长不含重复字符的子字符串
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 48. 最长不含重复字符的子字符串

## 题目描述

输入一个字符串（只包含 a\~z 的字符），求其最长不含重复字符的子字符串的长度。例如对于 arabcacfr，最长不含重复字符的子字符串为 acfr，长度为 4。

## 解题思路

```java
class Solution {
public:
    int longestSubstringWithoutDuplication(string s) {
        if(s.empty()) return 0;
        int len = s.size();
        int maxLen = 1;
        set<int> tmp;
        for(int i = 0; i < len; i ++)
        {
            tmp.clear();
            for(int j = i - 1; j >= 0; j --)
            {
                //cout <<"i: "<< i << " j: " << j << " " << s[j] << " ";
                if(s[j] == s[i] || !tmp.emplace(s[j] - '0').second) break;
               // cout <<"i: "<< i << " j: " << j << " " << s[j] <<" " << tmp.size()<< " ";
            }
            maxLen = max(maxLen, (int)tmp.size() + 1);
            //cout << " max: "<< maxLen << endl;
        }
        return maxLen;
    }
};
```





