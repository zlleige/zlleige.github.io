---
title: 剑指offer——14. 剪绳子
date: 2020-02-15 
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
- 贪心
- 动态规划
description: 剑指offer刷题
---

# 14. 剪绳子

[Leetcode](https://leetcode.com/problems/integer-break/description/)

## 题目描述

把一根绳子剪成多段，并且使得每段的长度乘积最大。

```html
n = 2
return 1 (2 = 1 + 1)

n = 10
return 36 (10 = 3 + 3 + 4)
```

## 解题思路

### 贪心

尽可能多剪长度为 3 的绳子，并且不允许有长度为 1 的绳子出现。如果出现了，就从已经切好长度为 3 的绳子中拿出一段与长度为 1 的绳子重新组合，把它们切成两段长度为 2 的绳子。

证明：当 n >= 5 时，3(n - 3) - n = 2n - 9 > 0，且 2(n - 2) - n = n - 4 > 0。因此在 n >= 5 的情况下，将绳子剪成一段为 2 或者 3，得到的乘积会更大。又因为 3(n - 3) - 2(n - 2) = n - 5 >= 0，所以剪成一段长度为 3 比长度为 2 得到的乘积更大。

```java
class Solution {
public:
    int maxProductAfterCutting(int length) {
        return greedSolution(length);
    }
    
    //贪心
    int greedSolution(int len)
    {
        if(len < 1) return -1;
        else if(len == 2) return 1;
        else if(len == 3) return 2;
        int nums3 = len / 3; //尽量多分成3 
        //求len对3的余数，0、2：不管  1：说明余数4  此时应该拆分为2 * 2
        if(len - nums3 * 3 == 1) 
        {
            nums3 -= 1;
        }
        int nums2 = (len - nums3 * 3) / 2;  //可以得到余下2的个数 主要存在两种情况（余下4 =》2*2 余下5=》3*2）
        return (int)pow(3,nums3) * (int)pow(2,nums2);
    }
};


class Solution {
public:
    int integerBreak(int n) {
        if (n <= 3) return 1 * (n - 1);
        int res = 1;
        if (n % 3 == 1) res = 4, n -= 4;
        else if (n % 3 == 2) res = 2, n -= 2;
        while (n) res *= 3, n -= 3;
        return res;
    }
};

class Solution {
    public int cuttingRope(int n) {
        if(n <=3) return n - 1;
        // 讨论n%3的余数，找规律
        int mod = n % 3;
        int c = n / 3;
        if(mod == 1) {
            // 4 7 10   (1,3)->(2,2)
            return (int)Math.pow(3, c-1) * 2 *2;
        } else if(mod == 2) {
            // 5 8
            return (int)Math.pow(3, c) * 2;
        } else {
            // 6 9
            return (int)Math.pow(3, c);
        }
    }
}
```

### 动态规划

```java
class Solution {
public:
    int maxProductAfterCutting(int length) {
        //return greedSolution(length);
        
        return dpSolution(length);
    }
    
    //dp
    int dpSolution(int len)
    {
        if(len < 1) return -1;
        else if(len == 2) return 1;
        else if(len == 3) return 2;
        int *dp = new int[len + 1]; //存入结果
        //初始化 比如 dp(4)=max(dp(1,3), dp(2,2))  表示当前len（>4）长度的绳子分成所有情况的最大值
        //之所以 0-3 对应的dp[i] = i;是为了组合len》3的情况下的长度，不是说要将len在分开。dp即为当前不分割的长度（即为本身长度）
        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 2;
        dp[3] = 3;
        int maxD = 0;
        //从下至上计算，保存当前的值 dp(n) = max(f(j)* f(n-j)); 对应j循环得到最大值
        for(int i = 4; i <= len; i  ++)
        {
            maxD = 0;  //初始为0
            for(int j = 1; j <= i/2; j ++) //j在1-i/2即可获得所有的情况  比如 dp(4)=max(dp(1,3), dp(2,2))
            {
                maxD = max(maxD, dp[j] * dp[i - j]);
            }
            dp[i] = maxD; //存下最大值
        }
        maxD = dp[len];
        delete[] dp;
        return maxD;
    }
```







## 剪绳子 2

```
答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，
2 <= n <= 1000
```



```java
class Solution {
    public int cuttingRope(int n) {
        if (n <= 3) {
            return n - 1;
        }

        //最大int 2147483647，为防止在某一次 mul乘3已经溢出，类型需要设为long
        long mul = 1;

        //3,3,3,3,3,4
        //3,3,3,3,3,3
        //3,3,3,3,3,2
        //3,3,3,3,3,1  X 此种情况算在和前面 3+1 和为 4
        while (n > 4) {
            //每次乘积后取余防止大数
            mul = mul * 3 % 1000000007;

            n -= 3;
        }
        return (int) (mul * n % 1000000007);
    }
}

```

