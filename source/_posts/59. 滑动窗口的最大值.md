---
title: 剑指offer——59. 滑动窗口的最大值
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 59. 滑动窗口的最大值

[NowCoder](https://www.nowcoder.com/practice/1624bc35a45c42c0bc17d17fa0cba788?tpId=13&tqId=11217&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

给定一个数组和滑动窗口的大小，找出所有滑动窗口里数值的最大值。

例如，如果输入数组 {2, 3, 4, 2, 6, 2, 5, 1} 及滑动窗口的大小 3，那么一共存在 6 个滑动窗口，他们的最大值分别为 {4, 4, 6, 6, 6, 5}。

## 解题思路

```java
/*
维护一个单调递减的队列
每次插入一个就输出一个

*/

class Solution {
public:
    vector<int> maxInWindows(vector<int>& nums, int k) {
        vector<int> vRes;
        deque<int> q; //双端队列 存数组下标
        //边界
        if(k > nums.size()) k = nums.size();
        //遍历数组
        for(int i = 0; i < nums.size(); i ++)
        {
            //判断是否队首已经滑出窗口 删除滑出的数据 eg: k=3 index=3 时 front=0 应该判断  即相隔了3个数  之后应该加入一个删除一个  
            while(!q.empty() && i-q.front() >= k)  q.pop_front();
            //维护一个递减序列  因为[2, 3, 4, 2, 6, 2, 5, 1] 加入到   [4,2] 添加6时，2，4<6 应该被滑出 因为4，2均不会被选中
            while(!q.empty() && nums[q.back()] <= nums[i]) q.pop_back(); 
            //加入序列
            q.push_back(i);
            //输出 当i = k-1之后 每次插入一个就输出一个 eg:index=2时 应该输出一项数据
            if( i >= k - 1) vRes.emplace_back(nums[q.front()]);
        }
        return vRes;
    }
};
```



