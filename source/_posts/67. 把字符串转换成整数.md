---
title: 剑指offer——67. 把字符串转换成整数
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 67. 把字符串转换成整数

## 题目链接

[NowCoder](https://www.nowcoder.com/practice/1277c681251b4372bdef344468e4f26e?tpId=13&tqId=11202&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

将一个字符串转换成一个整数，字符串不是一个合法的数值则返回 0，要求不能使用字符串转换整数的库函数。

```html
Iuput:
+2147483647
1a33

Output:
2147483647
0
```

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



