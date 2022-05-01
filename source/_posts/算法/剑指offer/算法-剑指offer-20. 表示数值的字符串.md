---
title: 剑指offer——20. 表示数值的字符串
date: 2020-02-15  
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 20. 表示数值的字符串

[NowCoder](https://www.nowcoder.com/practice/6f8c901d091949a5837e24bb82a731f2?tpId=13&tqId=11206&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

```
true

"+100"
"5e2"
"-123"
"3.1416"
"-1E-16"
```

```
false

"12e"
"1a3.14"
"1.2.3"
"+-5"
"12e+4.3"
```


## 解题思路

使用正则表达式进行匹配。

```html
[]  ： 字符集合
()  ： 分组
?   ： 重复 0 ~ 1 次
+   ： 重复 1 ~ n 次
*   ： 重复 0 ~ n 次
.   ： 任意字符
\\. ： 转义后的 .
\\d ： 数字
```

```java
public boolean isNumeric(char[] str) {
    if (str == null || str.length == 0)
        return false;
    return new String(str).matches("[+-]?\\d*(\\.\\d+)?([eE][+-]?\\d+)?");
}
```



我的做法：

```c++
/*
分情况讨论
1、去空格
2、去首字母 + -
2、排除非法情况
    非法数据 0-9 e/E . + -
  a、首位再次出现+-
  b、当e或E前面没有数字时，整个字符串不能表示数字，例如.e1、e1；
  c\当e或E后面没有整数时，整个字符串不能表示数字，例如12e、12e+5.4; 不能出现.
  d\只能出现
  e\小数点的个数 e的最多一个 右边不能有
  
  //牛客
   bool isNumeric(char* string)
    {
        std::string s = string;

*/

class Solution {
public:
    bool isNumber(string s) {
        if(s.empty())  return false;
        
        //出空格
        int i = 0, j = s.size() - 1;
        while(s[i] == ' ' && i < s.size()) i ++;
        while(s[i] == ' ' && j >= 0) j --;
        if(i > j) return false;
        s = s.substr(i, j - i + 1);

        //去首字母 + -
        if(s[0] == '+' || s[0] == '-') 
        {
            if(s.size() <=1) return false;
            s = s.substr(1);
        } 
        if(s[0] == '+' || s[0] == '-' || s[0] == '.' && s.size() <=1) return false; //多个符号 并且只有 一个点
      
        //定义符号数据 e . e后面的+—符号
        int eNums = 0, dotNums = 0, e_signNums = 0;
        //排除非法情况
        for(int i = 0; i < s.size(); i ++)
        {

            //cout << "sss1" << endl;

            //非法字符判断 0-9 +- .
            if(s[i] != '+' && s[i] != '-' && s[i] != '.' && s[i] != 'e' && s[i] != 'E' && !(s[i] >= '0' && s[i] <= '9')) return false;

            //.e1、e1
            if(s[i] == 'e' || s[i] == 'E') 
            {
                //cout << "sss3" << endl;
                eNums ++; if(eNums > 1) return false;
                if(i == 0 || i == 1 && s[0] == '.' || i == s.size() - 1 ) return false;  //例如.e1、e1；12e e+
                //cout << "sss3" <<eNums << i << endl;
            }
            
            //cout << "sss2" << endl;
            //小数点最多有一个 1.2.3  //e 后面的 12e+5.4   //允许 .12 233. //单独一个 '.'
            if(s[i] == '.') 
            {    
                dotNums ++;
                if(dotNums > 1 || dotNums == 1 && (eNums == 1 || s.size() <=1 )) return false;
            }

            //符号 因为排除了最开始的情况 所以符号数最多为1 且只能在e之后 5+4 
            if(s[i] == '+' || s[i] == '-') 
            {
                e_signNums ++;
                if(e_signNums > 1 || e_signNums == 1 && eNums <= 0 || eNums == 1 && i == s.size() - 1 ) return false;  //e+
            }
        }
        
        return true;
    }
};
```






