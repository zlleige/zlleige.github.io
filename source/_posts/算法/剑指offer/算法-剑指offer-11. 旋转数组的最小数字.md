---
title: 剑指offer——11. 旋转数组的最小数字
date: 2020-02-15   
categories:
- [算法, 剑指offer]
tags:
- 算法
- 剑指offer
description: 剑指offer刷题
---

# 11. 旋转数组的最小数字

[NowCoder](https://www.nowcoder.com/practice/9f3231a991af4f55b95579b44b7a01ba?tpId=13&tqId=11159&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking&from=cyc_github)

## 题目描述

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/0038204c-4b8a-42a5-921d-080f6674f989.png" width="210px"> </div><br>

## 解题思路

将旋转数组对半分可以得到一个包含最小元素的新旋转数组，以及一个非递减排序的数组。新的旋转数组的数组元素是原数组的一半，从而将问题规模减少了一半，这种折半性质的算法的时间复杂度为 O(logN)（为了方便，这里将 log<sub>2</sub>N 写为 logN）。

<div align="center"> <img src="https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/424f34ab-a9fd-49a6-9969-d76b42251365.png" width="300px"> </div><br>

**分析：**

1、交换前：单调递增，但是可能存在相同数的情况

![img](C:\Users\lenovo\AppData\Local\YNote\data\m18428365094_1@163.com\8b40652667604dc7b2b107a1db2368a8\clipboard.png)

2、交换后：整个数组从左至右分成两段，最初和最末可能出现相同的值

![img](C:\Users\lenovo\AppData\Local\YNote\data\m18428365094_1@163.com\c643ef7e854a47388202de025382667f\clipboard.png)

3、可以从后往前删掉与nums[0]相同的数据，得到后半部分单调

考虑两种情况：

![img](C:\Users\lenovo\AppData\Local\YNote\data\m18428365094_1@163.com\ec2ebcd559c24717b44c0d2f31c25067\clipboard.png)

4、二分数组下标 

数组[0-n], l=0,r=n  mid=l+r>>1;

if(nums[mid]>nums[0])  证明当前的mid在上图的左边，应该选择右边取最小值

```c++
class Solution {
public:
    int findMin(vector<int>& nums) {
        if(nums.empty()) return -1;
        int len = nums.size() - 1;
        //1--删除旋转后 最后部分与nums[0]的相同部分
        while (len > 0 && nums[len] == nums[0]) len -- ;
        //2--判断此时的数组是否单调(nums[0]最小)，还是分成了两段
        if(nums[len] >= nums[0]) return nums[0];
        //3--二分找出最小的位置
        int l = 0, r = len;  //对应小标
        while(l < r)
        {
            int mid = l + r >> 1; //区间 [l,mid] [mid + 1, r]
            if(nums[mid] < nums[0]) r = mid;  //在左边
            else l = mid + 1;
        }
        return nums[l];
    }
};
```





### java 实现



[leetcode题解]([旋转数组的最小数字 - 旋转数组的最小数字 - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/solution/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-by-leetcode-s/))



```java
class Solution {
    public int minArray(int[] num) {
        // 旋转后，存在最小值x，使得左侧数据>=x，右侧数据<=x.满足二分性质
        int low = 0, high = num.length -1;

        // 第三种情况：可能存在[22222 012222]此时mid会有和high相同的情况，但是无法判断是在左右区间，所以可以提前处理相同的数据
        while(high > 0 && num[high] == num[low]) {
            high --;
        }
        if(num[high] >= num[low]) return num[low];

        while(low < high) {
            int mid = low + (high -low)/2;
            if (num[mid] <= num[high]) {
                // 第一种情况：mid小于high,最小值在左边，但此时mid可能为最小值，取high=mid;
                high = mid; 
            } else if(num[mid] > num[high]){
                // 第二种情况：mid大于high,最小值在右边，但此时mid不可能为最小值，取low=mid+1;
                low = mid + 1; 
            }
        } 
        return num[high];
        
    }
}
```

