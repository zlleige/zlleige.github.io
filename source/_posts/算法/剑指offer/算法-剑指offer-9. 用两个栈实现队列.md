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



### java 实现 leetcode



简单明了，带你直接看懂题目和例子。 输入： ["CQueue","appendTail","deleteHead","deleteHead"] 这里是要执行的方法，从左到右执行

[[],[3],[],[]]对应上面的方法，是上面方法的参数。CQueue和deleteHead方法不需要指定数字，只有添加才需要指定数字

1.创建队列，返回值为null

2.将3压入栈，返回值为null

3.将栈底的元素删除，也就是消息队列中先进来的元素，所以是deleteHead，返回该元素的数值，所以为3

4.继续删除栈底的元素，但是没有元素了，所以返回-1

所以就有了下面的输出 输出：[null,null,3,-1]

示例 2： 输入： ["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]

[[],[],[5],[2],[],[]]

1.创建队列，返回值为null

2.删除栈底的元素，但是没有元素，所以返回-1

3.把5压入栈，返回null

4.把2压入栈，返回null

5.删除栈底的一个元素，也就是消息队列中先进来的元素，所以是deleteHead，就是最先进来的5，返回值为5，

6.删除栈底的一个元素，就是后进来的2，返回值为2，

所以就有了下面的输出

输出：[null,-1,null,null,5,2]

有没有发现先进来的数字，首先显示出来了，但是题目中说要使用栈，栈是先进后出的，使用栈来实现先进先出，在这里使用两个栈就好了，从一个进来再到另一个栈，这样顺序就是先进先出了。题目的主旨写在第一句，就是，使用两个栈实现一个队列。



```java
class CQueue {
    
    // s1接受数据，s2输出数据，当s2为空时，添加s1数据
    private Stack<Integer> s1,s2;
    
    public CQueue() {
        s1 = new Stack();
        s2 = new Stack();
    }
    
    public void appendTail(int value) {
        s1.push(value);
    }
    
    public int deleteHead() {
       if(!s2.empty()) {
           return s2.pop();
       } else {
           // 装s1数据
           while(!s1.empty()) {
               s2.push(s1.pop());
           }
           return s2.empty()?-1:s2.pop();
       }
    }

}

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */
```





