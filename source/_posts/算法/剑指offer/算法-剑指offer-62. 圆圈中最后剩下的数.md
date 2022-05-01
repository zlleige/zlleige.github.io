---
title: 剑指offer——62. 圆圈中最后剩下的数
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 62. 圆圈中最后剩下的数

## 题目链接

[NowCoder](https://www.nowcoder.com/practice/f78a359491e64a50bce2d89cff857eb6?tpId=13&tqId=11199&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

让小朋友们围成一个大圈。然后，随机指定一个数 m，让编号为 0 的小朋友开始报数。每次喊到 m-1 的那个小朋友要出列唱首歌，然后可以在礼品箱中任意的挑选礼物，并且不再回到圈中，从他的下一个小朋友开始，继续 0...m-1 报数 .... 这样下去 .... 直到剩下最后一个小朋友，可以不用表演。

## 解题思路

约瑟夫环，圆圈长度为 n 的解可以看成长度为 n-1 的解再加上报数的长度 m。因为是圆圈，所以最后需要对 n 取余。

```java
/*
思路一：时间：O(MN) 空间：O(n) 
用list构建循环链表  
定义一个指针循环数 找到m-1的位置
删除数据 直到list只剩下1个元素
**/
#include <list>
class Solution {
public:
    int lastRemaining(int n, int m){
        if(n <= 0 || m < 0 ) return -1;
        std::list<int>  data;
        for(int i = 0; i < n; i ++) data.emplace_back(i);
        auto current = data.begin();
        while(data.size() > 1)
        {
            //找到删除位置
            for(int i = 0; i < m - 1; i ++)  //0 1 2 3 4 删除第m=3个，依次删除 2 0 4 1 所以i《m
            {
                current ++;
                if(current == data.end()) current = data.begin();
            }
            auto next = ++ current;
            if(next == data.end()) next = data.begin();
            data.erase(--current); 
            current = next;
        }
        return *current;
    }
};

#if 1
/*
思路二：时间：O(n) 空间 0(1)
递推关系：
f(n,m)=(f(n-1,m)+m)%n  n>1
       0  n=1(只有一个0)
**/

class Solution {
public:
    //递归
    int lastRemaining1(int n, int m){
        if(n <= 1 || m < 0 ) return n-1;
        return  (lastRemaining(n - 1, m) + m) % n;
    }
    
    //迭代
    int lastRemaining(int n, int m){
        if(n <= 1 || m < 0 ) return n - 1;
        int last = 0;
        //数字是从1-n
        for(int i = 2; i <= n; i++) //一次递归i初始i=0 last=0  i=2 last=(last + m) % 2
        {
            last = (last + m) % i;
        }
        return last;
    }
};
#endif
```





