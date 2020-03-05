---
title: LeetCode011盛最多水的容器
copyright: true                                                                                                                                
date: 2019-03-04 16:41:41
tags: [数组,双指针,算法,LeetCode]
categories:
- LeetCode
- medium
top:
---

#### 题目描述
给定 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

说明：你不能倾斜容器，且 n 的值至少为 2。
<!--more-->

```tex
示例:

输入: [1,8,6,2,5,4,8,3,7]
输出: 49

```

---
#### 建议答案

```java
public int maxArea(int[] height) {
        int max = 0;
        int left = 0;
        int right = height.length - 1;
        while (left < right) {
            max = Math.max(max, Math.min(height[left], height[right]) * (right - left));
            if (height[right] > height[left]) {
                left++;
            } else {
                right--;
            }
        }
        return max;
    }
```

---
#### 思考

```java
public int maxArea(int[] height) {
        int max = 0;
        int left = 0;
        int right = height.length - 1;
        while (left < right) {
            max = Math.max(max, Math.min(height[left], height[right]) * (right - left));
            if (height[right] > height[left]) {
                left++;
            } else {
                right--;
            }
        }
        return max;
    }
```

> 双指针
> 面积总是由短的一方决定的，将指针放在两端，得到的面积与保存的最大面积进行比较，之后，开始移动。
> 将较短的一边向里移动

[证明](https://leetcode.com/problems/container-with-most-water/discuss/6099/yet-another-way-to-see-what-happens-in-the-on-algorithm)