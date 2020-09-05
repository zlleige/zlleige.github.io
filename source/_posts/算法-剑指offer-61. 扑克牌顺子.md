---
title: 剑指offer——61. 扑克牌顺子
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 61. 扑克牌顺子

## 题目链接

[NowCoder](https://www.nowcoder.com/practice/762836f4d43d43ca9deb273b3de8e1f4?tpId=13&tqId=11198&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

五张牌，其中大小鬼为癞子，牌面为 0。判断这五张牌是否能组成顺子。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/eaa506b6-0747-4bee-81f8-3cda795d8154.png" width="350px"> </div><br>


## 解题思路

```java
/*
O(nlogn)

**/
class Solution {
public:
    bool IsContinuous( vector<int> num ) {
        if(num.empty()) return false;
        //排序
        sort(num.begin(), num.end());
        //统计0的个数
        int index = 0;
        int zeroNum = 0;
        while(num[index] == 0)
        {
            index ++;
            zeroNum ++;
        }
        #if 0
        //统计空格数目
        int spaceNum = 0;
        for(int i = index; i < num.size() - 1; i ++)
        {
            int space  = num[i+1] - num[i];
            if(0 == space) return false;
            spaceNum += space - 1;
            if(spaceNum > zeroNum) return false;
        }
        #endif
        //直接判断
        return true;
    }
};
```





