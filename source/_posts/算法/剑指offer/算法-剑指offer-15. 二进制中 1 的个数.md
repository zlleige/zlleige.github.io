---
title: 剑指offer——15. 二进制中 1 的个数
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
- 位运算
description: 剑指offer刷题
---

# 15. 二进制中 1 的个数

[NowCoder](https://www.nowcoder.com/practice/8ee967e43c2c4ec193b040ea7fbb10b8?tpId=13&tqId=11164&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

输入一个整数，输出该数二进制表示中 1 的个数。

### n&(n-1)

该位运算去除 n 的位级表示中最低的那一位。

```
n       : 10110100
n-1     : 10110011
n&(n-1) : 10110000
```

时间复杂度：O(M)，其中 M 表示 1 的个数。



```c++
class Solution {
public:
    int NumberOf1(int n) {
        int nums = 0;
        //注意对于n！=0的判断
        for(int i = 0; i < 32 && n != 0; i ++)
        {
            nums += n & 1;
            n = n >> 1; //前位补0  
            //cout << n << " ";
        }
         //cout <<endl;
         return nums;
    }
};

//改进
class Solution {
public:
    int NumberOf1(int n) {
        int res = 0;
        unsigned int un = n; 
        while (un) res += un & 1, un >>= 1;
        return res;
    }
};
```





#### 方法一：循环检查二进制位

**思路及解法**

我们可以直接循环检查给定整数 *n* 的二进制位的每一位是否为 1。

具体代码中，当检查第 *i* 位时，我们可以让 *n* 与 2*i* 进行与运算，当且仅当 *n* 的第 *i* 位为 1 时，运算结果不为 0。

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int res = 0;
        for(int i =0; i < 32; i ++){
            if((n & (1 << i)) != 0) {
                res ++;
            }
        }
        return res;
    }
}
```



#### 方法二：位运算优化

**思路及解法**

观察这个运算：*n* & (*n*−1)，其预算结果恰为把 *n* 的二进制位中的最低位的 1 变为 0 之后的结果。

如：6 & (6−1)=4,6=(110)2,4=(100)2，运算结果 4 即为把 6 的二进制位中的最低位的 1 变为 0 之后的结果。

这样我们可以利用这个位运算的性质加速我们的检查过程，在实际代码中，我们不断让当前的 *n* 与 *n*−1 做与运算，直到 *n* 变为 0 即可。因为每次运算会使得 *n* 的最低位的 1 被翻转，因此运算次数就等于 *n* 的二进制位中 1 的个数。



```jav
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int res = 0;
        while(n != 0) {
            n &= n -1;
            res ++;
        }
        return res;
    }
}
```

