---
title: 剑指offer——65. 不用加减乘除做加法
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 65. 不用加减乘除做加法

## 题目链接

[NowCoder](https://www.nowcoder.com/practice/59ac416b4b944300b617d4f7f111b215?tpId=13&tqId=11201&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

写一个函数，求两个整数之和，要求不得使用 +、-、\*、/ 四则运算符号。

## 解题思路

a ^ b 表示没有考虑进位的情况下两数的和，(a & b) << 1 就是进位。

递归会终止的原因是 (a & b) << 1 最右边会多一个 0，那么继续递归，进位最右边的 0 会慢慢增多，最后进位会变为 0，递归终止。

```java
/*
O(32)
num1 + num2 = 直接加值 + 进位值
num1 + num2 = (num1^num2) + (num1&num2) << 1 = sum + carry;
循环：让sum1 = sum sum2 = carry; 一直求加  直到sum2=carry=0；
**/

class Solution {
public:
    int add(int num1, int num2){
        int sum = 0, carry = 0;
        do
        {
            sum = num1 ^ num2;
            carry = (num1 & num2) << 1;
            //构建下一次相加
            num1 = sum;  //sum1为最终结果
            num2 = carry;
        }while(num2 != 0);
        return num1;
    }
   
};
```




