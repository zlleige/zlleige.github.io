---
title: 剑指offer——66. 构建乘积数组
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 66. 构建乘积数组

## 题目链接

[NowCoder](https://www.nowcoder.com/practice/94a4d381a68b47b7a8bed86f2975db46?tpId=13&tqId=11204&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

给定一个数组 A[0, 1,..., n-1]，请构建一个数组 B[0, 1,..., n-1]，其中 B 中的元素 B[i]=A[0]\*A[1]\*...\*A[i-1]\*A[i+1]\*...\*A[n-1]。要求不能使用除法。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/4240a69f-4d51-4d16-b797-2dfe110f30bd.png" width="250px"> </div><br>


## 解题思路

```java
class Solution {
public:
    int strToInt(string str) {
        long long  res = 0;
        if(str.empty()) return res;
        //去空格
        int index = 0;
        while(index < str.size() && str[index] == ' ') index ++;
        //去± 做标记
        bool isMinus = false;
        if(str[index] == '+') index ++;
        else if(str[index] == '-') 
        {
            index ++;
            isMinus = true;
        }
        //构建整数
        for(int i = index; i < str.size(); i ++)
        {
            if(str[i] >= '0' && str[i] <= '9')
            {
                res = res * 10 + str[i] - '0';
            }
            else break; //不合法 跳出 
        }
        if(isMinus) res *= -1;
        if(res < INT_MIN) res = INT_MIN;
        if(res > INT_MAX) res = INT_MAX;
        return (int)res;
    }
};
```





