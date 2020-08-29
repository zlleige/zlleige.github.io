---
title: 剑指offer——41.1 数据流中的中位数
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 41.1 数据流中的中位数

[NowCoder](https://www.nowcoder.com/practice/9be0172896bd43948f8a32fb954e1be1?tpId=13&tqId=11216&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

## 解题思路

```java
/**
思路：
定义大顶堆和小顶堆 maxHeap minHeap
首先从大顶堆插入数据  
判断需要插入小顶堆的情况
1 maxHeap的容量大于minHeap.size() + 1; 此时应该插入minHeap
2 保证maxHeap top 始终小于minHeap.top()

**/
class Solution {
public:
    
    void insert(int num){
         maxHeap.emplace(num); //直接插入大根堆
        //判断当前数据 如果出现大根堆大于小根的情况 交换
        if(!maxHeap.empty() && !minHeap.empty() &&  maxHeap.top() >  minHeap.top() )
        {
            auto tmp = minHeap.top();
            minHeap.pop();
            minHeap.push(maxHeap.top());
            maxHeap.pop();
            maxHeap.push(tmp);
        }
        //数据多于1 转移到小根堆
        if(maxHeap.size() > minHeap.size() + 1) //数据入minHeap
        {
            minHeap.emplace(maxHeap.top());
            maxHeap.pop();
        }
    }

    double getMedian(){
        return maxHeap.size() == minHeap.size() ? (minHeap.top() + maxHeap.top()) / 2.0 : maxHeap.top();
    }
    
private:
    //定义大顶堆和小顶堆
    priority_queue<int> maxHeap;
    priority_queue<int, vector<int>, greater<int>> minHeap;
    
};
```





