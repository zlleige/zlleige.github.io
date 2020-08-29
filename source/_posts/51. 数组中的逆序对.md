---
title: 剑指offer——51. 数组中的逆序对
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 51. 数组中的逆序对

[NowCoder](https://www.nowcoder.com/practice/96bd6684e04a44eb80e6a68efc0ec6c5?tpId=13&tqId=11188&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

## 解题思路

```java
//归并排序求逆序对
    int mergesort(vector<int> & nums, int l, int r)
    {
        if(l >= r) return 0;
        //归并两个区间
        int mid = l + r >> 1;
        int res = 0;
        res += mergesort(nums,l, mid); //左边的逆序对
        res += mergesort(nums,mid + 1, r); //右边的逆序对
        
        //合并  需要辅助空间
        static vector<int> tmp;
        tmp.clear();
        int i = l, j = mid + 1;
        while(i <= mid && j <= r)
        {
            if(nums[i] <= nums[j]) tmp.push_back(nums[i ++]);
            else //存在逆序对
            {
                //左右两边区间都是排序的 i-[l, mid] [mid + 1. r] 证明i之后的值都会大于nums[j]
                res += mid - i + 1;
                tmp.push_back(nums[j ++]);
            }
        }
        //残余数据
        while(i <= mid) tmp.push_back(nums[i ++]);
        while(j <= r) tmp.push_back(nums[j ++]);
        //更新辅助数据到原数组
        for(i = l, j = 0; j < tmp.size(); i ++, j ++ ) nums[i] = tmp[j];
        return res;
    }
    
    int inversePairs(vector<int>& nums) {
        if(nums.empty()) return 0;
        return mergesort(nums,0, nums.size() - 1);
        
    }
```




