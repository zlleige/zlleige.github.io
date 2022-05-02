---
title: 剑指offer——5. 替换空格
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 5. 替换空格

## 题目链接

[牛客网](https://www.nowcoder.com/practice/4060ac7e3e404ad1a894ef3e17650423?tpId=13&tqId=11155&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述


将一个字符串中的空格替换成 "%20"。

```text
Input:
"A B"

Output:
"A%20B"
```

## 解题思路

① 在字符串尾部填充任意字符，使得字符串的长度等于替换之后的长度。因为一个空格要替换成三个字符（%20），所以当遍历到一个空格时，需要在尾部填充两个任意字符。

② 令 P1 指向字符串原来的末尾位置，P2 指向字符串现在的末尾位置。P1 和 P2 从后向前遍历，当 P1 遍历到一个空格时，就需要令 P2 指向的位置依次填充 02%（注意是逆序的），否则就填充上 P1 指向字符的值。从后向前遍是为了在改变 P2 所指向的内容时，不会影响到 P1 遍历原来字符串的内容。

③ 当 P2 遇到 P1 时（P2 <= P1），或者遍历结束（P1 < 0），退出。



<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/f7c1fea2-c1e7-4d31-94b5-0d9df85e093c.gif" width="350px"> </div><br>

```c++
class Solution {
public:
	void replaceSpace(char *str,int length) {
        int spaceNum = 0;
        for(int i = 0; i < length; i ++)
            if(str[i] == ' ') spaceNum ++;
        if(spaceNum == 0) return;
        int newLen = length + spaceNum * 2;
        for(int i = newLen, j = length; i >= 0 && j >= 0; j --)
        {
            if(str[j] == ' ')
            {
                str[i --] = '0';
                str[i --] = '2';
                str[i --] = '%';
             }
            else 
            {
                 str[i --] = str[j];
            }
        }
	}
};
```



java实现:

时间复杂度O(N),空间复杂度 O(N)

```java
class Solution {
    public String replaceSpace(String s) {
        // 获取当前的空格数
        int sLen = s.length();
        int spaceCount = 0;
        for(int i=0;i<sLen;i++) {
            if(s.charAt(i) == ' ') spaceCount ++;
        }
        // 初始化一个字符数组空间
        int newLen = sLen + 2*spaceCount;
        char[] newStr = new char[newLen];
        //从后往前复制数据
        for(int i = newLen-1, j = sLen-1; i>=0 && j >=0; j --){
            if(s.charAt(j) != ' ') {
                newStr[i--] = s.charAt(j);
            } else {
                newStr[i--] = '0';
                newStr[i--] = '2';
                newStr[i--] = '%';
            }
        }
        return new String(newStr, 0, newLen);
    }
}
```



