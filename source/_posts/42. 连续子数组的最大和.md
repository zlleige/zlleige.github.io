---
title: 剑指offer——42. 连续子数组的最大和
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 42. 连续子数组的最大和

[NowCoder](https://www.nowcoder.com/practice/459bd355da1549fa8a49e350bf3df484?tpId=13&tqId=11183&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

{6, -3, -2, 7, -15, 1, 2, 2}，连续子数组的最大和为 8（从第 0 个开始，到第 3 个为止）。

## 解题思路

```java
/*
dp:s表示当前位置i前面的一个子数组的最大长度  res：存入各个子数组和的最大值
f(i) = nums[i] i = 0 || f(i - 1 < 0)
       f(i - 1) + nums[i] i ≠ 0 && f(i - 1) > 0
遍历数组：记录s的值 如果s < 0, 证明当前的子数组必须更新  s = x; 否则s += x; 每次s都要更新res
***/

class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        if(nums.empty()) return INT_MIN; //#include <climits> 
        int s = 0, res = INT_MIN;
        for(auto x : nums)
        {
            if(s < 0) s = 0; //这里的处理技巧  如果s<0, 就抛弃以前的数据 
            s += x;
            res = max(res, s);
        }
        return res;
    }
};
```







