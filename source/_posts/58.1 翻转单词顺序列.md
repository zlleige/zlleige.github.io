---
title: 剑指offer——58.1 翻转单词顺序列
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 58.1 翻转单词顺序列

[NowCoder](https://www.nowcoder.com/practice/3194a4f4cf814f63919d0790578d51f3?tpId=13&tqId=11197&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

```html
Input:
"I am a student."

Output:
"student. a am I"
```

## 解题思路

题目应该有一个隐含条件，就是不能用额外的空间。虽然 Java 的题目输入参数为 String 类型，需要先创建一个字符数组使得空间复杂度为 O(N)，但是正确的参数类型应该和原书一样，为字符数组，并且只能使用该字符数组的空间。任何使用了额外空间的解法在面试时都会大打折扣，包括递归解法。

正确的解法应该是和书上一样，先旋转每个单词，再旋转整个字符串。

```java
class Solution {
public:
    string reverseWords(string s) {
        if(s.empty()) return "";
        reverse(s.begin(), s.end());
        auto it1 = s.begin();
        auto it2 = s.begin(); //左闭又开
        while(it2 != s.end())
        {
            if(*it2 == ' ') 
            {
                reverse(it1, it2);
                it1 =  ++ it2;
            }
            else it2 ++;
        }
        reverse(it1, it2);
        return s;
    }
};

//飞库函数版本
class Solution {
public:
    string reverseWords(string s) {
        if(s.empty()) return s;
        for(int i = 0, j = s.size() - 1; i < j; i ++, j --) swap(s[i], s[j]);
        int k = 0; //记录最后一个空格位置
        for(int i = 0, j = 0; j < s.size(); j ++)
        {
            if(s[j] == ' ') 
            {
                for(int m = i, n = j - 1; m < n; m ++, n --) swap(s[m], s[n]);
                i = k = j + 1;
            }
        }
        if(k < s.size())
        {
            for(int i = k, j = s.size() - 1; i < j; i ++, j --) swap(s[i], s[j]);
        }
        return s;
    }
};
```







