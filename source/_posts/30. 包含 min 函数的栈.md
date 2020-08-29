---
title: 剑指offer——30. 包含 min 函数的栈
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 30. 包含 min 函数的栈

[NowCoder](https://www.nowcoder.com/practice/4c776177d2c04c2494f2555c9fcc1e49?tpId=13&tqId=11173&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

定义栈的数据结构，请在该类型中实现一个能够得到栈最小元素的 min 函数。

## 解题思路

```java
/*
思路：
用一个辅助栈，每次压栈的时候，存入栈顶和压入数据的最小值，弹出时也弹出
这样就可以记录每一次压栈的时最小值状态

**/
class MinStack {
public:
    /** initialize your data structure here. */
    MinStack() {
        
    }
    void push(int x) {
        //数据栈压入数据
        _data.push(x);
        //辅助栈压入最小数据
        if(_minData.empty()) _minData.push(x);
        else _minData.push(min(_minData.top(), x));
    }
    void pop() {
        if(_data.empty()) return;
        _data.pop();
        _minData.pop();
    }
    int top() {
        return _data.top();
    }
    int getMin() {
        return _minData.top();
    }
private:
    int _min = INT_MIN;
    stack<int> _data;
    stack<int> _minData;
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```





