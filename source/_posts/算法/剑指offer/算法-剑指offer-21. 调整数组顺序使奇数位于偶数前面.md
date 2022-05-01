---
title: 剑指offer——21. 调整数组顺序使奇数位于偶数前面串
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 21. 调整数组顺序使奇数位于偶数前面

[NowCoder](https://www.nowcoder.com/practice/beb5aa231adc45b2a5dcc5b62c93f593?tpId=13&tqId=11166&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

需要保证奇数和奇数，偶数和偶数之间的相对位置不变，这和书本不太一样。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/d03a2efa-ef19-4c96-97e8-ff61df8061d3.png" width="200px"> </div><br>

## 解题思路



**分析：**

(双指针扫描) O(n)O(n)

用两个指针分别从首尾开始，往中间扫描。扫描时保证第一个指针前面的数都是奇数，第二个指针后面的数都是偶数。

每次迭代时需要进行的操作：

第一个指针一直往后走，直到遇到第一个偶数为止；

第二个指针一直往前走，直到遇到第一个奇数为止；

交换两个指针指向的位置上的数，再进入下一层迭代，直到两个指针相遇为止；

时间复杂度

当两个指针相遇时，走过的总路程长度是 n，所以时间复杂度是 O(n)。

```c++
class Solution {
public:
    void reOrderArray(vector<int> &array) {
         
         int len = array.size() - 1;
         if(len <= 0) return;
         //两个指针 分别头和尾  遇到不同的即交换
         int l = 0, r = len; 
         while(l < r)
         {
             //cout << array[l] % 2 << array[r] % 2<< endl;
             //判断条件
             //1 左边为偶数同时右边为奇数 交换 首尾指针前移
             //2 左边为偶 右边不为奇数  r--
             //3 左边为奇数 右边为奇数 l ++
             //4 其余情况 指针靠近
             if(array[l] % 2 == 0 && array[r] % 2 ==1)
             {
                 swap(array[l],array[r]);
                 l ++;
                 r --;
             }
             else if(array[l] % 2 == 0) r --; 
             else if(array[r] % 2 == 1) l ++;
             else 
             {
                 l ++;
                 r --;
             }
         }
    }
};


//优化

void reOrderArray(vector<int> &array) {
        int i=0,j=array.size()-1;
        while(i<j){
            while(i<j && array[i]%2==1) i++;  //直到找到第一个奇数
            while(i<j && array[j]%2==0) j--;  //直到找到第一个偶数
            if(i<j) swap(array[i],array[j]);  //交换
        }
    }
```

