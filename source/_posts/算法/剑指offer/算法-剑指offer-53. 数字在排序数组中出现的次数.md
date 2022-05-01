---
title: 剑指offer——53. 数字在排序数组中出现的次数
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 53. 数字在排序数组中出现的次数

[NowCoder](https://www.nowcoder.com/practice/70610bf967994b22bb1c26f9ae901fa2?tpId=13&tqId=11190&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

```html
Input:
nums = 1, 2, 3, 3, 3, 3, 4, 6
K = 3

Output:
4
```

## 解题思路

```java
#include <unordered_map>
class Solution {
public:
    //二分
    int getNumberOfK(vector<int>& nums , int k) {
        if(nums.empty()) return 0;
        //0--找左端点
        int l =0, r = nums.size() - 1;
        while(l < r)
        {
            int mid = l + r >>1;
            if(nums[mid] < k) l = mid +1;
            else r = mid;
        }
        //此时找到值为k的左端点 l = r
        if(nums[l] != k) return 0; //判断是否存在k
        int left = l;
        
        //--找右端点
        l =0, r = nums.size() - 1;
        while(l < r)
        {
            int mid = l + r + 1>>1;
            if(nums[mid] <= k) l= mid;
            else r = mid - 1;
        }
        
        return r - left + 1;
    }
    
    //hash On
    int getNumberOfK1(vector<int>& nums , int k) {
        unordered_map<int, int> hash;
        for(auto x : nums)
        {
            hash[x] ++;
        }
        return hash[k];
    }
};
```





