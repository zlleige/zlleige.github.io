---
title: 剑指offer——60. n 个骰子的点数
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 60. n 个骰子的点数

## 题目链接

[Lintcode](https://www.lintcode.com/en/problem/dices-sum/)

## 题目描述

把 n 个骰子扔在地上，求点数和为 s 的概率。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/195f8693-5ec4-4987-8560-f25e365879dd.png" width="300px"> </div><br>

## 解题思路

### 动态规划

使用一个二维数组 dp 存储点数出现的次数，其中 dp\[i]\[j] 表示前 i 个骰子产生点数 j 的次数。

空间复杂度：O(N<sup>2</sup>)

```java
class Solution {
public:
    vector<int> numberOfDice(int n) {
        vector<int>dp(6*n+1, 0);
        for(int i = 1;i<=6;i++)//动归数组初始值，表示1个骰子扔出1-6的可能数都为1
            dp[i] = 1;
        for(int i = 2;i<=n;i++){
            for(int j = 6*i;j>=0;j--){
                dp[j] = 0;
                for(int k = 6;k>=1;k--){//最后一个骰子可以扔1-6点
                    if(j-k<0)
                        continue;
                    dp[j] += dp[j-k];
                }
            }
        }
        vector<int>res(dp.begin()+n, dp.end());//扔n个骰子的和为[n, 6*n]
        return res;
    }
};
```



