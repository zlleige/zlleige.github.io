---
title: 剑指offer——4. 二维数组中的查找
date: 2020-02-15   
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 4. 二维数组中的查找

## 题目链接

[牛客网](https://www.nowcoder.com/practice/abc3fe2ce8e146608e868a70efebf62e?tpId=13&tqId=11154&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

给定一个二维数组，其每一行从左到右递增排序，从上到下也是递增排序。给定一个数，判断这个数是否在该二维数组中。

```html
Consider the following matrix:
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]

Given target = 5, return true.
Given target = 20, return false.
```

## 解题思路

要求时间复杂度 O(M + N)，空间复杂度 O(1)。其中 M 为行数，N 为 列数。

该二维数组中的一个数，小于它的数一定在其左边，大于它的数一定在其下边。因此，从右上角开始查找，就可以根据 target 和当前元素的大小关系来缩小查找区间，当前元素的查找区间为左下角的所有元素。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/35a8c711-0dc0-4613-95f3-be96c6c6e104.gif" width="400px"> </div><br>

```c++
class Solution {
public:
    bool Find(int target, vector<vector<int> > array) {
        if(array.empty() || array.at(0).empty()) return false;
        int N = array.size(), M = array[0].size();
        for(int i = 0, j = M - 1; i < N && j >= 0; )
        {
            if(array[i][j] == target) return true;
            else if(array[i][j] > target) j --;
            else i ++;
        }
        return false;
    }
};
```



### JAVA 实现

时间复杂度O(N),空间复杂度O(1)

从右上角的数据开始比较：

```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if(matrix ==null || matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }
        int row = matrix.length;
        int col = matrix[0].length;

        for(int j = col - 1, i = 0; j >= 0 && i < row; ) {
            if(matrix[i][j] == target) {
                return true;
            } else if(matrix[i][j] < target) {
                i ++;
            } else {
                j --;
            }
        }
        return false;
    }
}
```



