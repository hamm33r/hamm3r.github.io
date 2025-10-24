---
layout:       post
title:        "二分算法模板和一些细节问题"
author:       "hamm33r"
header-style: text
catalog:      true
tags:         binary_search
---
# 二分算法模板和一些细节问题
## 给出题目
[在排序数组中查找元素的第一个和最后一个位置](https://leetcode.cn/problems/find-first-and-last-position-of-element-in-sorted-array/description/)
当发现题目的解集具有**二分性**也就是要找的**x**在数组中可以划分为
> 大于等于x
> 小于x

 两块区间，这时就可以使用二分算法，二分算法的模板如下
 ```c++

 //二分查找区间左端点,假设2是要找的数，区间为左闭右开
 //a[] = [1, 1, 2, 2, 3, 4, 5, 5]
 //             ^        
 //查找左端点，所以在求mid时应该靠左
int l = 0, int r = n;
while(l < r)
{
    int mid = (l + r) / 2;
    if(a[mid] < x)
    l = mid + 1;
    else
    r = mid;
}
//程序结束后需要判断left或者right是否是想要的结果
 ```
 ```c++
  //二分查找区间右端点,假设2是要找的数
 //a[] = [1, 1, 2, 2, 3, 4, 5, 5]
 //                ^
int l = 0, int r = n;
while(l < r)
{
    int mid = (l + r + 1) / 2;
    if(a[mid] > x)
    r = mid - 1;
    else
    l = mid;
}
//程序结束后需要判断left或者right是否是想要的结果
 ```
## 细节问题
### 循环的判断条件
无论是求区间的左端点还是右端点，判断条件都是`while(l < r)`
举例`[2, 2]`若判断条件是`while(l <= r)`都会造成死循环
### 求中点的方式
`(l + r) / 2 和 (l + r + 1) / 2`区别在于当区间长度是偶数时，求出的中点一个偏左，一个偏右，当要查找的是区间的左端点，使用的是`(l + r) / 2`。这是配套的，查找区间的右端点时反之。
### left和right的迁移
> 求区间的左端点时，判断条件为`if(a[mid] < x)`因为不是<=,所以此时mid的左边是不会有x的，所以此时应该让`left = mid + 1`
> 
> 求区间右端点时`if(a[mid] > x )`,x不可能在mid的右边所以应让`right = mid - 1`

### 二分结束之后，相遇点的情况
`[2, 2]`无论是求区间左边端点还是右边端点，最终都会left = right,所以判断left或者right是否等于x即可

