---
title: 剑指offer——63. 股票的最大利润
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 63. 股票的最大利润

## 题目链接

[Leetcode：121. Best Time to Buy and Sell Stock ](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)

## 题目描述

可以有一次买入和一次卖出，买入必须在前。求最大收益。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/42661013-750f-420b-b3c1-437e9a11fb65.png" width="220px"> </div><br>

## 解题思路

使用贪心策略，假设第 i 轮进行卖出操作，买入操作价格应该在 i 之前并且价格最低。

```java
/*
题意分析：
买入卖出的时间点恰当 即招待前i个数中的最小值 用当前值与之相减比较

*/
class Solution {
public:
    int maxDiff(vector<int>& nums) {
        if(nums.empty()) return 0;
        int minNum = nums[0]; //定义一个最小值
        int res = 0;  //存入结果
        for(auto x : nums)
        {
            res = max(res, x - minNum);
            minNum = min(x, minNum);
        }
        return res;
    }
};
```





