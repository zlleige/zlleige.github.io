---
title: 剑指offer——49. 丑数
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 49. 丑数

[NowCoder](https://www.nowcoder.com/practice/6aa9e04fc3794f68acf8778237ba065b?tpId=13&tqId=11186&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

把只包含因子 2、3 和 5 的数称作丑数（Ugly Number）。例如 6、8 都是丑数，但 14 不是，因为它包含因子 7。习惯上我们把 1 当做是第一个丑数。求按从小到大的顺序的第 N 个丑数。

## 解题思路

```java
#if 1
/*
归并思想：对于关于2，3，5的抽数组归并去重
定义一个数组保存丑数 初始为1 
i j k 分别对应x2 x3 x5的数据更新，初始指向0，归并更新
使得每次添加的元数都是x2 x3 x5中最小的

丑数，这题可以理解为求取只包含2，3，5质数因为的数的从小到大的集合，可以考虑为一个三路归并的问题，
第一路是包含质因子2的所有数的集合，第二路是包含3的质因子的所有数的集合，同理，第三路是包含5的质因子的所有数的集合，
但是可以看出，这三路是有交集的，所以需要去重，还有就是需要指出的是此为只包含2,3,5质因子的集合。
就yxcls所说的题解来看，可以看出每一路的元素其实都在归并后的数组中，且这个数组可以保证其中的每个元素都是只包含2,3,5质因子。
**/
class Solution {
public:
    int getUglyNumber(int n) {
        if(n <= 1) return n;
        vector<int> v(1, 1); //数组保存丑数 初始为1
        int i = 0, j = 0, k = 0; //定义三个位置变量 分别对应x2 x3 x5的序列 用于更新数据
        //技巧 执行n-1次（第一位为1）
        while(--n)
        {
            int tmp = min(v[i] * 2, min(v[j] * 3, v[k] * 5)); //更新当前序列最小的值
            v.emplace_back(tmp);
            //更新坐标 兼容了三种情况出现相同的情景
            if(tmp == v[i] * 2) i ++;
            if(tmp == v[j] * 3) j ++;
            if(tmp == v[k] * 5) k ++;
        }
        return v.back();
    }
    
};
#endif


#if 0
/*
方法一：暴力解法 超时
1、从1开始判断是否为丑数， index++ 直到n
**/
class Solution {
public:
    int getUglyNumber(int n) {
        if(n <= 0) return 0;
        long data = 0; 
        int index = 0;
        while(index < n)
        {
            ++ data;
            if(isUglyNum(data)) ++ index;
        }
        return data;
    }
    
    //判断是否为丑数
    bool isUglyNum(int n)
    {
        while(n % 2 == 0) n /= 2;
        while(n % 3 == 0) n /= 3;
        while(n % 5 == 0) n /= 5;
        return n ==1 ;
    }
};
#endif

```





