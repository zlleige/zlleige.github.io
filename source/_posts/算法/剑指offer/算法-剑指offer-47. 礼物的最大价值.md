---
title: 剑指offer——47. 礼物的最大价值
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 47. 礼物的最大价值

[NowCoder](https://www.nowcoder.com/questionTerminal/72a99e28381a407991f2c96d8cb238ab)

## 题目描述

在一个 m\*n 的棋盘的每一个格都放有一个礼物，每个礼物都有一定价值（大于 0）。从左上角开始拿礼物，每次向右或向下移动一格，直到右下角结束。给定一个棋盘，求拿到礼物的最大价值。例如，对于如下棋盘

```
1    10   3    8
12   2    9    6
5    7    4    11
3    7    16   5
```

礼物的最大价值为 1+12+5+7+7+16+5=53。

## 解题思路

应该用动态规划求解，而不是深度优先搜索，深度优先搜索过于复杂，不是最优解。

```java
/*
动态规划：
1、状态表示
dp[i][j] 表示i行j列的最大值
2、状态转移表达式
dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]) + grid[i][j]
3、状态边界
dp[i][0] = dp[0][j] = 0 
dp[m][n] 结果
**/

class Solution {
public:
    int getMaxValue(vector<vector<int>>& grid) {
        if(grid.empty() || grid.at(0).empty()) return 0;
        int m = grid.size(), n = grid.at(0).size();
        vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0)); //初始边界dp[i][0] = dp[0][j] = 0
        for(int i = 1; i <= m; i ++)
            for(int j = 1; j <= n; j ++ )
            {
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]) + grid[i - 1][j - 1];
            }
        return dp[m][n];
    }
};
```





