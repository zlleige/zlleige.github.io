---
title: 剑指offer——39. 数组中出现次数超过一半的数字
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 39. 数组中出现次数超过一半的数字

[NowCoder](https://www.nowcoder.com/practice/e8a1b01a2df14cb2b228b30ee6a92163?tpId=13&tqId=11181&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 解题思路

多数投票问题，可以利用 Boyer-Moore Majority Vote Algorithm 来解决这个问题，使得时间复杂度为 O(N)。

使用 cnt 来统计一个元素出现的次数，当遍历到的元素和统计元素相等时，令 cnt++，否则令 cnt--。如果前面查找了 i 个元素，且 cnt == 0，说明前 i 个元素没有 majority，或者有 majority，但是出现的次数少于 i / 2 ，因为如果多于 i / 2 的话 cnt 就一定不会为 0 。此时剩下的 n - i 个元素中，majority 的数目依然多于 (n - i) / 2，因此继续查找就能找出 majority。

```java
/*
说明：
遍历数组，用两个变量记录状态 
val:记录当前的元素 用于返回
nums ：初始为1 消耗需求数据
如果当前值与前一个相同 nums++ 
如果当前值与前一个不同：num--  if(num==0) =>nums = 1 val = 当前的值

***/

class Solution {
public:
    int moreThanHalfNum_Solution(vector<int>& nums) {
        if(nums.empty()) return INT_MIN;
        int val = INT_MIN, n = 0;
        for(auto x : nums)
        {
            if(n == 0 ) n = 1, val = x;
            else if(x != val)
            {
                n --;
            }
            else n ++;
        }
        //验证是否为超过一半
        int hafNum = 0;
        for(auto x : nums)
        {
            if(x == val) hafNum ++;
        }
        
        return hafNum > nums.size() / 2 ? val: 0;
    }
};
```







