---
title: 剑指offer——16. 数值的整数次方
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 16. 数值的整数次方

[NowCoder](https://www.nowcoder.com/practice/1a834e5e3e1a4b7ba251417554e07c00?tpId=13&tqId=11165&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

给定一个 double 类型的浮点数 base 和 int 类型的整数 exponent，求 base 的 exponent 次方。

## 解题思路

下面的讨论中 x 代表 base，n 代表 exponent。

<!--<div align="center"><img src="https://latex.codecogs.com/gif.latex?x^n=\left\{\begin{array}{rcl}(x*x)^{n/2}&&{n\%2=0}\\x*(x*x)^{n/2}&&{n\%2=1}\end{array}\right." class="mathjax-pic"/></div> <br>-->

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/48b1d459-8832-4e92-938a-728aae730739.jpg" width="330px"> </div><br>


因为 (x\*x)<sup>n/2</sup> 可以通过递归求解，并且每次递归 n 都减小一半，因此整个算法的时间复杂度为 O(logN)。

```c++
#if 1
//迭代
class Solution {
public:
    double Power(double base, int exponent) {
        if(exponent == 0) return 1;
        bool isBig = exponent > 0; //标志当前的幂次正负
        if(!isBig) exponent = -exponent;
        double res = 1;
        while(exponent --) res *= base;
        
        return isBig ? res : 1 / res; 
    }
};

#endif


#if 0
/*
O(N)
pow(b,e)=
e=0 1;
e>0 b*pow(b,e-1)
e<0 1/(b*pow(b,e+1))
*/

class Solution {
public:
    double Power(double base, int exponent) {
        if(exponent == 0) return 1;
        else if(exponent > 0) return base * Power(base, --exponent );
        else 
        {
            exponent = -exponent;
            //cout << exponent << endl;
            return 1.0 / (base * Power(base, --exponent ));
        }
    }
};
#endif
```





