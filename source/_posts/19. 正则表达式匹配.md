---
title: 剑指offer——19. 正则表达式匹配
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 19. 正则表达式匹配

[NowCoder](https://www.nowcoder.com/practice/45327ae22b7b413ea21df13ee7d6429c?tpId=13&tqId=11205&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

请实现一个函数用来匹配包括 '.' 和 '\*' 的正则表达式。模式中的字符 '.' 表示任意一个字符，而 '\*' 表示它前面的字符可以出现任意次（包含 0 次）。

在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串 "aaa" 与模式 "a.a" 和 "ab\*ac\*a" 匹配，但是与 "aa.a" 和 "ab\*a" 均不匹配。

## 解题思路

应该注意到，'.' 是用来当做一个任意字符，而 '\*' 是用来重复前面的字符。这两个的作用不同，不能把 '.' 的作用和 '\*' 进行类比，从而把它当成重复前面字符一次。

```java
/*
动态规划：
状态：bool f[i][j] 表示s[i---] 能被p[j--]匹配的结果

状态转移：
1、p[j]为普通字符 f[i][j] = s[i][j] && f[i + 1][j + 1]
2、p[j]为'.' f[i][j] = f[i + 1][j + 1]  '.'表示一位数据
//1,2合并处理
3、p[j + 1]为'*' 如：'b*' *可以表示出现0次
   *表示0次时： f[i][j] = f[i][j + 2] 跳过这两个数据 "aaa"和"ab*ac*a"
   *表示b出现多次时： f[i][j] = f[i + 1][j] 就类似于暴力枚举  f[i + 1][j]的状态只比f[i][j] 少了* = 0 的状态 “abba”-“ab*a”

边界：f[n][m] = true;  表示跑完了 n=s.sise() m=p.sise()
实际处理 f设为int -1：表示初始化  true(1):表示能够匹配 false:表示不能匹配

**/
class Solution {
public:
    bool isMatch(string s, string p) {
        return match(s, p, 0 , 0, s.size(), p.size());
        //return match((char*)s.data(), (char*)p.c_str());
    }
    
    //x-s的索引 y-p的索引
    bool match(string& s, string& p, int x, int y, int sLen, int pLen)
    {
        //考虑空情况
        if(x == sLen && y == pLen) return true;
        //考虑第1 2种情况
        bool firstMatch = y < pLen && x < sLen &&( s[x] == p[y] || p[y] == '.');  //  "" 与 ".*" 匹配 所以不能一概 x<sLen
        if(firstMatch && match(s, p, x + 1, y + 1, sLen, pLen)) return true;
        //考虑第三种情况 *  (b*)
        if(y + 1 < pLen && p[y + 1] == '*')
        {
            //cout << "adf  " << x << y<< endl;
            //考虑*匹配0次和多次的情况
            if(match(s, p, x , y + 2, sLen, pLen) || (firstMatch && match(s, p, x + 1 , y, sLen, pLen))) return true;
        }
        return false;
    }
    bool match(char* str, char* pattern)
    {
        //排除都为空的情况
        if (pattern[0] == 0 && str[0] == 0)
        {
            return true;
        }
        //第一二种状态 
        bool firstMatch = (pattern[0] == '.' && str[0]) || str[0] == pattern[0];  // 此时要求str[0]有效  "" 与 ".*" 匹配 所以不能一概 x<sLen
        if (firstMatch && match(str + 1, pattern + 1))
             return true;
        //第三种情况  "b*..." 
        if (pattern[0] != 0 && pattern[1] == '*')
        {
            if ( match(str, pattern + 2) ||  (firstMatch && match(str + 1, pattern))) //转移到
                return true;
        }

        return false;   
    }
};
```






