---
title: 剑指offer——29. 顺时针打印矩阵
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 29. 顺时针打印矩阵

[NowCoder](https://www.nowcoder.com/practice/9b4c81a02cd34f76be2659fa0d54342a?tpId=13&tqId=11172&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

下图的矩阵顺时针打印结果为：1, 2, 3, 4, 8, 12, 16, 15, 14, 13, 9, 5, 6, 7, 11, 10

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/48517227-324c-4664-bd26-a2d2cffe2bfe.png" width="200px"> </div><br>

## 解题思路

空间复杂度 O(N) 保存状态

```java
/*
思路：
vector<int> res;
//1边界
if(!matrix.empty() || !matrix[0].empty()) return res;
//定义一个标记数组，记录是否路线访问 

int row = matrix.size(), col = matrix[0].size();
vector<vector<bool> > isVisited(row, vector<bool>(col, false));
 
//2定义两个向量 构造顺时针 x:表示上下 y：表示左后 
int dx[4] = {0, 1, 0, -1}, dy[4] = {1, 0 , -1, 0}; //以矩阵左上角为坐标原点游动 右上左下
0--------> 
-
-
-
-
//3遍历
int x = 0, y = 0 , d = 0; // index x:表示上下row  y:表示左右 col   d:表示方向向量的index 初始化为0 标志 向右移动
for(int i = 0; i < row * col; i ++)
{
    //装入数据 
    res.emplac_back(matrix[x][y]); 
    isVisited[x][y] = true;
    
    
    判断当前走到的点是否为边界
    int a = x + dx[d], b = y + dy[d];
    
    if(x >= row - 1 || x <= 0 || y >= col - 1 || y <= 0 || isVisited[x][y])
    {
        d = (d + 1) % 4; //更新一个方向
        a = x + dx[d];
        b = y + dy[d];
    }

    //更新坐标
    x = a; 
    y = b;
}

return res;

**/

class Solution {
public:
    vector<int> printMatrix(vector<vector<int> > matrix) {
        //边界判断
        vector<int> res;
        if(matrix.empty() || matrix[0].empty()) return res;
        //定义标记
        int row = matrix.size(), col = matrix[0].size();
        vector<vector<bool> > isVisited(row, vector<bool>(col, false));
        
        //定义循环向量 顺时针 左上右下
        int dx[4] = {0, 1, 0, -1}, dy[4] = {1, 0, -1, 0};
        //遍历 初始坐标x y 方向循环d
        int x = 0, y = 0, d = 0;
        for(int i = 0; i < row * col; i ++)
        {
            //装载数据
            res.emplace_back(matrix[x][y]);
            isVisited[x][y] = true;
            
            int a = x + dx[d], b = y + dy[d];
            //边界更新坐标 bianliguod
            if(a < 0 || a >= row  || b < 0 || b >= col || isVisited[a][b])
            {
                d = (d + 1) % 4; //循环方向
                a = x + dx[d], b = y + dy[d]; //更新数据
            }

            x = a;
            y = b;
        }
        return res;
    }
};
```





