---
title: LeetCode088合并两个有序数组
copyright: true
date: 2019-02-25 11:35:39
tags: [数组,双指针,LeetCode,算法]
categories: 
- LeetCode
- easy
top:
---

#### 题目描述

给定两个有序整数数组 nums1 和 nums2，将 nums2 合并到 nums1 中，使得 num1 成为一个有序数组。
<!--more-->

说明:

初始化 nums1 和 nums2 的元素数量分别为 m 和 n。
你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。

```tex
    示例:
    输入:
    nums1 = [1,2,3,0,0,0], m = 3
    nums2 = [2,5,6],       n = 3

    输出: [1,2,2,3,5,6]
```

---
#### 建议答案

```java
public void merge(int[] nums1, int m, int[] nums2, int n) {
        for (int i = nums1.length - 1; i >= 0; i--) {
            if (m == 0) {
                nums1[i] = nums2[--n];
            } else if (n == 0) {
                break;
            } else if (nums2[n - 1] > nums1[m - 1]) {
                nums1[i] = nums2[--n];
            } else {
                nums1[i] = nums1[--m];
            }
        }
    }
```



---
#### 思考

##### 逗比解法

```java
public int[] merge1(int[] nums1, int m, int[] nums2, int n) {
        System.arraycopy(nums2, 0, nums1, m, n);
        Arrays.sort(nums1);
        return nums1;
    }
```

##### 遍历判断

```java
public int[] merge(int[] nums1, int m, int[] nums2, int n) {
        for (int i = nums1.length - 1; i >= 0; i--) {
            if (m == 0) {
                nums1[i] = nums2[--n];
            } else if (n == 0) {
                return nums1;
            } else if (nums2[n - 1] > nums1[m - 1]) {
                nums1[i] = nums2[--n];
            } else {
                nums1[i] = nums1[--m];
            }
        }
        return nums1;
    }
```

>自写，已经运用到了前面一些题的思想，可喜可贺。