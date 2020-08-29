---
title: 剑指offer——56. 数组中只出现一次的数字
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 56. 数组中只出现一次的数字

[NowCoder](https://www.nowcoder.com/practice/e02fdb54d7524710a7d664d082bb7811?tpId=13&tqId=11193&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

一个整型数组里除了两个数字之外，其他的数字都出现了两次，找出这两个数。

## 解题思路

两个不相等的元素在位级表示上必定会有一位存在不同，将数组的所有元素异或得到的结果为不存在重复的两个元素异或的结果。

diff &= -diff 得到出 diff 最右侧不为 0 的位，也就是不存在重复的两个元素在位级表示上最右侧不同的那一位，利用这一位就可以将两个元素区分开来。

```java
class Solution {
public:
    vector<int> findNumsAppearOnce(vector<int>& nums) {
        vector<int> vRes;
        set<int> s;
        for(auto it = nums.begin(); it != nums.end(); it ++)
        {
            //重复出现
            if(!s.insert(*it).second)
            {
                s.erase(*it);
            }
        }
        if(s.size() != 2) return vRes;
        vRes.assign(s.begin(),s.end()); //重构
        return vRes;
    }
};
/**
该题解题思路
异或得到 x^y
取 x与y中第k位为1的数
将数分为两个集合，第k位为1的集合和第k位不是1的集合
其中x y分别在这两个集合，且相同的元素是在同一个集合里面
于是将其转化成了求重复数字中的单个数值的问题
*/

class Solution {
public:
    vector<int> findNumsAppearOnce(vector<int>& nums) {
        if(nums.empty()) return  vector<int>();
        int sum = 0; //x^y
        for(auto x : nums)
        {
            sum ^= x;
        }
        //找到x^y的任意一位为1的位
        int k = 0;
        while(k < nums.size() && !(sum >> k & 1)) k++;
        //再次轮循数组 与(sum >> k) & 1 异或就可以得到其中一个数字
        int d1 = 0;
        for(auto x : nums)
        {
            if(x >> k & 1)
                d1 ^= x;
        }
        //sum = x ^ y 
        return  vector<int>{d1, d1 ^ sum};
    }
};
```





