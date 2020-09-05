---
title: 剑指offer——57.2 和为 S 的连续正数序列
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 57.2 和为 S 的连续正数序列

[NowCoder](https://www.nowcoder.com/practice/c451a3fd84b64cb19485dad758a55ebe?tpId=13&tqId=11194&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

输出所有和为 S 的连续正数序列。

例如和为 100 的连续序列有：

```
[9, 10, 11, 12, 13, 14, 15, 16]
[18, 19, 20, 21, 22]。
```

## 解题思路

```java
//暴力
class Solution {
public:
    vector<vector<int> > findContinuousSequence(int sum) {
        vector<vector<int> > res;
        for(int i = 1; i < sum; i ++)
        {
            int tmp = i;
            vector<int> vTmp;
            for(int j = i + 1; j < sum; j ++)
            {
                tmp += j;
                if(tmp == sum)
                {
                    for(int k = i; k <= j; k++) vTmp.push_back(k);
                    res.push_back(vTmp);
                    break;
                }
                
            }
        }
        return res;
    }
};

//双指针做法  [i,j]表示i加到j的和位sum 下一个状态下 i增加 j应该增加
    vector<vector<int> > findContinuousSequence(int sum) {
        vector<vector<int> > res;
        int l = 1, r = l + 1;
        vector<int> vTmp;
        while(r < sum)
        {
            int tmp = (r - l + 1)*(l + r) / 2; //n* (a1+an)/2
            if(tmp < sum) r ++; //先累计右边
            else if(tmp == sum)
            {
                for(int i = l; i <= r; i ++) vTmp.emplace_back(i);
                res.emplace_back(vTmp);
                vTmp.clear();
                l ++;
            }
            else l ++;
        }
        return res;
    }
    
    class Solution {
public:
    vector<vector<int> > findContinuousSequence(int sum) {
        vector<vector<int>> res;
        vector<int> vTmp;
        int l = 1, r = l + 1;
        while(r < sum)
        {
            int s = (r - l + 1) * (r + l) / 2;
            if(s == sum) 
            {
                for(int i = l; i <= r; i ++) vTmp.push_back(i);
                res.push_back(vTmp);
                vTmp.clear();
            }
            if(s > sum) l ++;
            else r ++;
        }
        return res;
    }
};


```




