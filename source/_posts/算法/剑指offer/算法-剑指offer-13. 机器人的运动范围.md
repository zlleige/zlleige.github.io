---
title: 剑指offer——13. 机器人的运动范围
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 13. 机器人的运动范围

[NowCoder](https://www.nowcoder.com/practice/6e5207314b5241fb83f2329e89fdecc8?tpId=13&tqId=11219&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

地上有一个 m 行和 n 列的方格。一个机器人从坐标 (0, 0) 的格子开始移动，每一次只能向左右上下四个方向移动一格，但是不能进入行坐标和列坐标的数位之和大于 k 的格子。

例如，当 k 为 18 时，机器人能够进入方格 (35,37)，因为 3+5+3+7=18。但是，它不能进入方格 (35,38)，因为 3+5+3+8=19。请问该机器人能够达到多少个格子？

## 解题思路

使用深度优先搜索（Depth First Search，DFS）方法进行求解。回溯是深度优先搜索的一种特例，它在一次搜索过程中需要设置一些本次搜索过程的局部状态，并在本次搜索结束之后清除状态。而普通的深度优先搜索并不需要使用这些局部状态，虽然还是有可能设置一些全局状态。

```c++
//回溯法

class Solution {
public:
    int movingCount(int threshold, int rows, int cols)
    {
        if(rows <= 0 || cols <= 0) return 0;
        vector<vector<bool>> isVisited(rows, vector<bool>(cols, false)); //用于标记是否访问
        int count = movingCountCore(threshold, rows, cols, 0, 0, isVisited);
        return count;
    }
    
     int movingCountCore(int threshold, int rows, int cols, int row, int col, vector<vector<bool>>& isVisited)
     {
         if(row < 0 || row >= rows|| col < 0 || col >= cols || isVisited[row][col])
             return 0;
         else if(checkNums(threshold, row, col))
         {
             isVisited[row][col] = true;
             int dx[4] = {-1, 0, 1, 0}, dy[4] = {0, -1, 0 ,1}, res = 1;
             for(int i = 0; i< 4; i++)
                 res += movingCountCore(threshold, rows, cols, row + dx[i], col + dy[i], isVisited); //递归
             return res;
            // return 1 + movingCountCore(threshold, rows, cols, row -1, col, isVisited) 
            //         + movingCountCore(threshold, rows, cols, row , col -1, isVisited) 
            //         + movingCountCore(threshold, rows, cols, row + 1, col, isVisited) 
            //         + movingCountCore(threshold, rows, cols, row, col + 1, isVisited);
         }
         else return 0;
     }
     
     bool checkNums(int threshold, int row, int col)
     {
        int sum = 0;
        while(row > 0)
        {
            sum += row % 10;
            row /= 10;
        }
        while(col > 0)
        {
            sum += col % 10;
            col /= 10;
        }
        return sum <= threshold;
     }
};

//牛客网  bool *
class Solution {
public:
    int movingCount(int threshold, int rows, int cols)
    {
        if(rows <= 0 || cols <= 0) return 0;
        bool* isVisited = new bool[rows * cols]; //用于标记
        for(int i = 0; i < rows * cols; i ++) //初始化
        {
            isVisited[i] = false; 
        }
        int count = movingCountCore(threshold, rows, cols, 0, 0, isVisited);
        delete[] isVisited;
        return count;
    }
    int movingCountCore(int threshold, int rows, int cols, int row, int col, bool* isVisited)
    {
        if(row < 0 || row >= rows || col < 0 || col >= cols || isVisited[row * cols + col] ) return 0;
        if(checkNums(threshold, row, col))
        {
            isVisited[row * cols + col] = true;
            int dx[4] = {-1, 0, 1, 0}, dy[4] = {0, -1, 0, 1}, res = 1;
            for(int i = 0; i < 4; i ++)
            {
                res += movingCountCore(threshold, rows, cols,row + dx[i], col + dy[i], isVisited);
            }
            return res;
        }
        else return 0;
    }
    
    bool checkNums(int threshold, int row, int col)
    {
        int sum = 0;
        while(row > 0)
        {
            sum += row % 10; //各位数和
            row /= 10;
        }
        while(col > 0)
        {
            sum += col % 10; //各位数和
            col /= 10;
        }
        return sum <= threshold;
    }
};
```





### java 实现

DFS：



```java
class Solution {
    public int movingCount(int m, int n, int k) {
        // dfs
        if(m < 0 || n < 0 || k <0)  {
            return 0;
        }
        boolean vis[][] = new boolean[m][n];
        return dfs(m, n, 0, 0, k,vis);
    }
    
    private int dfs(int m, int n, int x, int y, int k, boolean[][] vis) {
        // 边界条件
        if(x <0 || x >= m || y<0 || y >=n || vis[x][y] || !isVisit(x, y, k) ) {
            return 0;
        }
        // 当前位置记录可达
        vis[x][y] = true;
        // 遍历四个方向，可达数据之和返回
        int dx[] = {-1, 0, 1, 0}; 
        int dy[] = {0, -1, 0, 1};
        int res = 1;
        for (int i = 0; i < 4; i ++) {
            int nx = x + dx[i];
            int ny = y + dy[i];
            res += dfs(m, n, nx, ny,k,vis);
        }
        // return 1 + dfs(m, n, x +1, y,k,vis) +dfs(m, n, x -1, y,k,vis) +dfs(m, n, x, y+1,k,vis) +dfs(m, n, x, y-1,k,vis);

        return res;
    }

    private int getSum (int x) {
        int sum = 0;
        while(x > 0) {
            sum += x % 10;
            x /= 10;
        }
        return sum;
    }

    private boolean isVisit(int x, int y, int k) {
        return getSum(x) +getSum(y) <= k;
    }


}
```

