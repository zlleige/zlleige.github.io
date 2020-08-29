---
title: 剑指offer——9. 用两个栈实现队列点
date: 2020-02-15   
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 9. 用两个栈实现队列

## 题目链接

[牛客网](https://www.nowcoder.com/practice/54275ddae22f475981afa2244dd448c6?tpId=13&tqId=11158&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

用两个栈来实现一个队列，完成队列的 Push 和 Pop 操作。

## 解题思路

in 栈用来处理入栈（push）操作，out 栈用来处理出栈（pop）操作。一个元素进入 in 栈之后，出栈的顺序被反转。当元素要出栈时，需要先进入 out 栈，此时元素出栈顺序再一次被反转，因此出栈顺序就和最开始入栈顺序是相同的，先进入的元素先退出，这就是队列的顺序。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/3ea280b5-be7d-471b-ac76-ff020384357c.gif" width="450"/> </div><br>

```c++
class MyQueue {
public:
    /** Initialize your data structure here. */
    MyQueue() {
        
    }
    
    /** Push element x to the back of queue. */
    void push(int x) {
        stack1.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        copy(stack1, stack2);
        int res = stack2.top();
        stack2.pop();
        copy(stack2, stack1);
        return res;
    }
    
    /** Get the front element. */
    int peek() {
        copy(stack1, stack2);
        int res = stack2.top();
        copy(stack2, stack1);
        return res;
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        return stack1.empty();
    }
    
    void copy(stack<int>& stack1, stack<int>& stack2)
    {
        while(stack1.size())
        {
            stack2.push(stack1.top());
            stack1.pop();
        }
    }
private:
    stack<int> stack1;
    stack<int> stack2;
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * bool param_4 = obj.empty();
 */
```





