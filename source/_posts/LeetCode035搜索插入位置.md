---
title: LeetCode035搜索插入位置
copyright: true
date: 2019-02-22 19:20:14
tags: [LeetCode,数组,二分查找,算法,移位运算]
categories: 
- LeetCode
- easy
top:
---

#### 题目描述：
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。
<!--more-->

```tex
示例 1:

输入: [1,3,5,6], 5
输出: 2

示例 2:

输入: [1,3,5,6], 2
输出: 1

示例 3:

输入: [1,3,5,6], 7
输出: 4

示例 4:

输入: [1,3,5,6], 0
输出: 0
```

---
#### 建议答案：

```java
public static int searchInsert(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int start = 0;
        int end = nums.length;  
        while (start < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] < target) {
                start = mid + 1;
            } else {
                end = mid;      
            }
        }
        return start;
    }
```

---
#### 思考：

##### 1. 简单算法：

```java
  public static int searchInsert(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            if (target <= nums[i]) {
                return i;
            }
        }
        return nums.length;
    }
```
>元素少的时候效率高
>非通解，取巧



##### 2. 二分查找：

```java
public static int searchInsert(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int start = 0;
        int end = nums.length;  
        while (start < end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] < target) {
                start = mid + 1;
            } else {
                end = mid;      
            }
        }
        return start;
    }
```
>通常解


##### 3. 二分查找：

```java
public static int searchInsert(int[] nums, int target) {
        int begin = 0, end = nums.length - 1, mid = 0;
        while (begin <= end) {
            mid = (begin + end) >>> 1;//相当于(begin + end) / 2
            if (nums[mid] < target) {  
                begin = mid + 1;      //一定要是begin在前面判断
            } else if (nums[mid] > target) {
                end = mid - 1;
            } else {
                return mid;
            }	
        }
        if (begin == 0 || begin == nums.length) {
            return begin;
        } else {
            return ((begin + end) >>> 1) + 1;
        }
    }
```
>通常情况下比较好的解
>需要列出所有可能的情况考虑
>1. 对于一般情况：
如果存在，直接返回，无疑义。
如果不存在，迭代到最后一步时，如
target = 4，   3，5 ，此时，判断，target>｛3｝，begin=mid+1，begin与end相等，继续判断，target<｛5｝，end=mid-1，结束。那么，返回结果，（begin+end）/2+1。
>2. 对于特殊情况：
没有元素的，返回0，即begin。
只有一个元素的:
如果目标小于元素，按begin=0的情况处理，返回0或begin。
如果在右边，按begin为len的情况处理，返回begin。
在两边之外的:
如果在左边，begin始终为0，end最后为-1,那么返回0或者begin。
如果在右边，end始终为len-1，begin最后为len，那么需要返回begin。
综上，如果begin=0，返回begin，如果begin为len，也返回begin，如果为其它情况，返回（begin+end）/2+1。

---
#### 测试用例：

```java
        System.out.println(searchInsert(new int[]{1, 3, 5, 6}, 5));  //2
        System.out.println(searchInsert(new int[]{1, 3, 5, 6}, 2));  //1
        System.out.println(searchInsert(new int[]{1, 3, 5, 6}, 7));  //4
        System.out.println(searchInsert(new int[]{1, 3, 5, 6}, 0));  //0
        System.out.println(searchInsert(new int[]{1, 3, 5, 6}, 1));  //0
        System.out.println(searchInsert(new int[]{}, 1));            //0
        System.out.println(searchInsert(new int[]{2}, 1));           //0
        System.out.println(searchInsert(new int[]{1}, 1));           //0
        System.out.println(searchInsert(new int[]{1}, 3));           //1
        System.out.println(searchInsert(new int[]{1, 3}, 2));        //1
```

---
#### 总结:
二分查找不熟练，回去学《算法》去。



