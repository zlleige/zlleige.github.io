---
title: 剑指offer——31. 栈的压入、弹出序列
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 31. 栈的压入、弹出序列

[NowCoder](https://www.nowcoder.com/practice/d77d11405cc7470d82554cb392585106?tpId=13&tqId=11174&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。

例如序列 1,2,3,4,5 是某栈的压入顺序，序列 4,5,3,2,1 是该压栈序列对应的一个弹出序列，但 4,3,5,1,2 就不可能是该压栈序列的弹出序列。

## 解题思路

使用一个栈来模拟压入弹出操作。

```java
/*
思路：
开一个辅助栈：
0、边界
若两个序列长度不等则视为并不是一个栈的压入、弹出序列。若两个序列都为空，则视为是一个栈的压入、弹出序列。
if(pushV.size() != popV.size() ) return false;
if( push.empty() && push.empty()) return true;

1、输入序列 [1,2,3,4,5] 输出序列[4,5,3,2,1]
依次遍历输出序列 x（4），当栈顶元素不为x时，将输入序列压栈直到找到x,并且将x弹出

//结束条件
当输出序列为空 -return true;
当输入序列为空-并且栈顶数据不匹配输出序列 false

**/
class Solution {
public:
    bool isPopOrder(vector<int> pushV,vector<int> popV) {
        if(pushV.size() != popV.size() ) return false;
        if( pushV.empty() && popV.empty()) return true;
        stack<int> sta;
        
        auto itPush = pushV.begin();
        auto itPop = popV.begin();
       
        while(itPush != pushV.end())
        {
            //加入数据
           sta.push(*itPush);
           itPush ++;
           //弹出数据
           while(!sta.empty() && sta.top() == *itPop)
           {
               sta.pop();
               itPop ++;
           }
        }
        return sta.empty();
    }
};
```





