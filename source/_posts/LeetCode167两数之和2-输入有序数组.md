---
title: LeetCode167两数之和2-输入有序数组
copyright: true
date: 2019-02-26 15:43:33
tags: [数组,双指针,二分查找,LeetCode,算法]
categories:
- LeetCode
- easy
top:
---

#### 题目描述
给定一个已按照升序排列 的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2。

<!--more-->

说明:

返回的下标值（index1 和 index2）不是从零开始的。
你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

```tex
示例:

输入: numbers = [2, 7, 11, 15], target = 9
输出: [1,2]
解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。
```

---
#### 建议答案

```java
 public int[] twoSum(int[] nums, int target) {
        if (numbers == null || numbers.length == 0) return new int[2];
        int temp;
        int len = nums.length - 1;
        for (int i = 0; i <= len; i++) {
            temp = target - nums[i];
            while (nums[len] >= temp) {
                if (temp == nums[len]) return new int[]{i + 1, len + 1};
                len--;
            }
        }
        throw new RuntimeException();
    }
```

---
#### 思考

##### 1.双指针碰撞

```java
 public int[] twoSum(int[] nums, int target) {
        if (numbers == null || numbers.length == 0) return new int[2];
        int temp;
        int len = nums.length - 1;
        for (int i = 0; i <= len; i++) {
            temp = target - nums[i];
            while (nums[len] >= temp) {
                if (temp == nums[len]) return new int[]{i + 1, len + 1};
                len--;
            }
        }
        throw new RuntimeException();
    }
```

>1ms,正常人能想到的方法

##### 2.二分查找 

```java
public int[] twoSum(int[] numbers, int target) {
        if (numbers == null || numbers.length == 0) {
            return new int[2];
        }
        int start = 0;
        int end = numbers.length - 1;
        while (start < end) {
            if (numbers[start] + numbers[end] == target) {
                return new int[]{start + 1, end + 1};
            } else if (numbers[start] + numbers[end] > target) {
                end = largestSmallerOrLastEqual(numbers, start, end, target - numbers[start]);
            } else {
                start = smallestLargerOrFirstEqual(numbers, start, end, target - numbers[end]);
            }
        }
        return new int[2];
    }
    
    private int largestSmallerOrLastEqual(int[] numbers, int start, int end, int target) {
        int left = start;
        int right = end;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (numbers[mid] > target) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        return right;
    }
    
    private int smallestLargerOrFirstEqual(int[] numbers, int start, int end, int target) {
        int left = start;
        int right = end;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (numbers[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return left;
    }
```

>0ms，二分查找不熟练的话很容易晕。
>我一开始就是这个思路，结果把自己写晕了。