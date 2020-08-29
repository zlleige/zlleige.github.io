---
title: 剑指offer——58.2 左旋转字符串
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 58.2 左旋转字符串

[NowCoder](https://www.nowcoder.com/practice/12d959b108cb42b1ab72cef4d36af5ec?tpId=13&tqId=11196&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

```html
Input:
S="abcXYZdef"
K=3

Output:
"XYZdefabc"
```

## 解题思路

先将 "abc" 和 "XYZdef" 分别翻转，得到 "cbafedZYX"，然后再把整个字符串翻转得到 "XYZdefabc"。

```java
/*

输入："abcdefg" , n=2
考虑先将字符串倒个 "gfedc ba" 可以尝试两次倒装
输出："cdefgab"

*/

#if 1 //使用库函数
class Solution {
public:
    string leftRotateString(string str, int n) {
        if(str.empty() || n < 0 || n > str.size()) return str;
        for(int i = 0, j = str.size() - 1; i < j; i ++, j --) swap(str[i], str[j]);
        for(int i = 0, j = str.size() - n - 1 ; i < j; i ++, j --) swap(str[i], str[j]);
        for(int i = str.size() - n, j = str.size() - 1; i < j; i ++, j --) swap(str[i], str[j]);
        return str;
    }
};
#endif

#if 0 //使用库函数
class Solution {
public:
    string leftRotateString(string str, int n) {
        if(str.empty() || n < 0 || n > str.size()) return str;
        reverse(str.begin(), str.end());
        reverse(str.begin(), str.end() - n); //左闭区间 右开
        reverse(str.end() - n, str.end());
        return str;
    }
};
#endif
```


