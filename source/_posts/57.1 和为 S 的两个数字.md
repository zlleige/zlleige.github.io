---
title: 剑指offer——57.1 和为 S 的两个数字6. 数组中只出现一次的数字
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 57.1 和为 S 的两个数字

[NowCoder](https://www.nowcoder.com/practice/390da4f7a00f44bea7c2f3d19491311b?tpId=13&tqId=11195&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

输入一个递增排序的数组和一个数字 S，在数组中查找两个数，使得他们的和正好是 S。如果有多对数字的和等于 S，输出两个数的乘积最小的。

## 解题思路

使用双指针，一个指针指向元素较小的值，一个指针指向元素较大的值。指向较小元素的指针从头向尾遍历，指向较大元素的指针从尾向头遍历。

- 如果两个指针指向元素的和 sum == target，那么得到要求的结果；
- 如果 sum > target，移动较大的元素，使 sum 变小一些；
- 如果 sum < target，移动较小的元素，使 sum 变大一些。

```java
class Solution {
public:
    vector<int> findNumbersWithSum(vector<int>& nums, int target) {
        //用hash
        unordered_set<int> hash;
        for(int i = 0; i < nums.size(); i ++)
        {
            hash.insert(nums[i]);
            if(hash.count(target - nums[i])) return vector<int>{target - nums[i],nums[i]};
        }
        return vector<int>();
    }
    
    vector<int> findNumbersWithSum1(vector<int>& nums, int target) {
        for(int i = 0; i < nums.size(); i ++)
            for(int j = i + 1; j < nums.size(); j ++)
                if(nums[i] + nums[j] == target) return vector<int>{nums[i],nums[j]};
        return vector<int>();
    }
};
```





