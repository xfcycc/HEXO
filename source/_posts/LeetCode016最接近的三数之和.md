---
title: LeetCode016最接近的三数之和
copyright: true
date: 2019-03-14 16:59:59
tags: [数组,双指针,LeetCode,算法]
categories:
- LeetCode
- medium
top:
---

#### 题目

给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的

和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

<!--more-->

```tex

例如，给定数组 nums = [-1，2，1，-4], 和 target = 1.

与 target 最接近的三个数的和为 2. (-1 + 2 + 1 = 2).

```

-------
#### 答案

```java
public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int result = nums[0] + nums[1] + nums[2];
        for (int i = 0; i < nums.length - 2; i++) {//不用遍历到最后一个数就已经全部判断完了
            int left = i + 1;
            int right = nums.length - 1;
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (Math.abs(sum - target) < (Math.abs(result - target))) {
                    result = sum;
                }
                if (sum < target) {
                    left++;
                } else if (sum > target) {
                    right--;
                } else {
                    return sum;
                }
            }
        }
        return result;
    }
```

利用的三数之和的思想，先排序，找出首尾上的数，将结果与目标相比，不断接近目标值。