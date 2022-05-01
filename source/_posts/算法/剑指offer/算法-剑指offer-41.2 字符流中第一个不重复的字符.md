---
title: 剑指offer——41.2 字符流中第一个不重复的字符
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 41.2 字符流中第一个不重复的字符

[NowCoder](https://www.nowcoder.com/practice/00de97733b8e4f97a3fb5c680ee10720?tpId=13&tqId=11207&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符 "go" 时，第一个只出现一次的字符是 "g"。当从该字符流中读出前六个字符“google" 时，第一个只出现一次的字符是 "l"。

## 解题思路

```java
/*
哈希表
 
**/
class Solution
{
public:
  //Insert one char from stringstream
    void Insert(char ch)
    {
         str.append(1, ch);   
    }
  //return the first appearence once char in current stringstream
    char FirstAppearingOnce()
    {
        char res = '#';
        if(str.empty()) return res;
        unordered_map<char, int> dat;
        for(auto x : str)
        {
            dat[x] ++;
        }
        for(auto x : str)
        {
            if(dat[x] == 1)
            {
                res = x; break;
            }
        }
        return res;
    }
private:
    string str;
};
```





