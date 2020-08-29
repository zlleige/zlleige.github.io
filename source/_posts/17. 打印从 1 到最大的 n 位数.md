---
title: 剑指offer——17. 打印从 1 到最大的 n 位数
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 17. 打印从 1 到最大的 n 位数

## 题目描述

输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数即 999。

## 解题思路

由于 n 可能会非常大，因此不能直接用 int 表示数字，而是用 char 数组进行存储。

使用回溯法得到所有的数。

```java
#include <iostream>
 
using namespace std;
 
void PrintMaxNDigits(int n);
void PrintToMaxNDigits(char *number, int index);
void PrintNumber(char *number);
 
int main() {
    int n;
    while(cin>>n) PrintMaxNDigits(n);
    return 0;
}
 
void PrintMaxNDigits(int n) { //n位上的0-9的全排列问题
    if (n <= 0) return;
    char *number = new char[n + 1];
    memset(number, '0', n);
    number[n] = '\0'; //末尾，用字符串时，高位在前，低位在后存
    while(!Increment(number)) PrintNumber(number);
    delete[]number;
}
 
void Increment(char *number) { //加法模拟
    bool IsOF =false;
    int CV = 0, len = strlen(number);
    for(int i = len-1; i>=0; --i) {
        int sum = number[i]-'0'+CV;
        if(i == len-1) sum++;
        if(sum >= 10) {
            if(i == 0) IsOF = true;
            else {
                sum -= 10;
                CV = 1;
                number[i] = '0'+sum;
            }
        } else {
            number[i] = '0'+sum;
            break;
        }
    }
    return IsOF;
}
 
void PrintNumber(char *number) { //输出 
    int len=strlen(number); 
    bool tag=true; 
    for(int i=0; i<len; i++) { 
        if(tag&&number[i]!='0') tag=false; //高位为0的不输出 
        if(!tag) cout<<number[i]; 
    } 
    if(!tag) cout<<endl; 
}
```



全排列：

```c++
#include <iostream>
 
using namespace std;
 
void PrintMaxNDigits(int n);
void PrintToMaxNDigits(char *number, int index);
void PrintNumber(char *number);
 
int main() {
    int n;
    while(cin>>n) PrintMaxNDigits(n);
    return 0;
}
 
void PrintMaxNDigits(int n) { //n位上的0-9的全排列问题
    if (n <= 0) return;
    char *number = new char[n + 1];
    number[n] = '\0'; //末尾，用字符串时，高位在前，低位在后存
    PrintToMaxNDigits(number, n, 0); //已修改，比之前更简洁 
    delete[]number;
}
 
void PrintToMaxNDigits(char *number, int index) { //递归的过程
    int len = strlen(number);
    if (index == len) {   //递归终止条件
    	PrintNumber(number);  //打印出当前的数字 
    	return;
    }
    for (int i = 0; i < 10; i++) {  //递归分支，当前数取0~9 
    	number[index] = i + '0';
    	PrintToMaxNDigits(number, len, index + 1);  //递归深度
    }
}
 
void PrintNumber(char *number) { //输出 
    int len = strlen(number), index = 0;;
    while(index < len && number[i] == '0') ++index; //高位为0的不输出
    if(index < len) {
        while(index < len) cout << number[i]; 
        cout << endl;
    }
}
```



> 参考：[https://blog.csdn.net/qq_15711195/article/details/94651798]

