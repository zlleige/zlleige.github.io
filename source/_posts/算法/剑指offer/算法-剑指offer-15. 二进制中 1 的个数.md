---
title: 剑指offer——15. 二进制中 1 的个数
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 15. 二进制中 1 的个数

[NowCoder](https://www.nowcoder.com/practice/8ee967e43c2c4ec193b040ea7fbb10b8?tpId=13&tqId=11164&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

输入一个整数，输出该数二进制表示中 1 的个数。

### n&(n-1)

该位运算去除 n 的位级表示中最低的那一位。

```
n       : 10110100
n-1     : 10110011
n&(n-1) : 10110000
```

时间复杂度：O(M)，其中 M 表示 1 的个数。



```c++
class Solution {
public:
    int NumberOf1(int n) {
        int nums = 0;
        //注意对于n！=0的判断
        for(int i = 0; i < 32 && n != 0; i ++)
        {
            nums += n & 1;
            n = n >> 1; //前位补0  
            //cout << n << " ";
        }
         //cout <<endl;
         return nums;
    }
};

//改进
class Solution {
public:
    int NumberOf1(int n) {
        int res = 0;
        unsigned int un = n; 
        while (un) res += un & 1, un >>= 1;
        return res;
    }
};
```







