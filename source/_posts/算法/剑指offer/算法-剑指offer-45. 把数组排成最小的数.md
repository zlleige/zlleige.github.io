---
title: 剑指offer——45. 把数组排成最小的数
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 45. 把数组排成最小的数

[NowCoder](https://www.nowcoder.com/practice/8fecd3f8ba334add803bf2a06af1b993?tpId=13&tqId=11185&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。例如输入数组 {3，32，321}，则打印出这三个数字能排成的最小数字为 321323。

## 解题思路

可以看成是一个排序问题，在比较两个字符串 S1 和 S2 的大小时，应该比较的是 S1+S2 和 S2+S1 的大小，如果 S1+S2 < S2+S1，那么应该把 S1 排在前面，否则应该把 S2 排在前面。

```java
class Solution {
public:
    string printMinNumber(vector<int>& nums) {
        if(nums.empty() ) return "";
        sort(nums.begin(), nums.end(), cmp);
        string str;
        for(auto x : nums)
        {
            str += to_string(x);
        }
        return str;
    }
    
    //回调
    static bool cmp(int a, int b)
    {
        return to_string(a) + to_string(b) < to_string(b) + to_string(a);
    }
};
```





