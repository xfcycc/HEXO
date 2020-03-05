---
title: LeetCode053最大子序和
copyright: true
date: 2019-02-23 08:28:10
tags: [算法,LeetCode,数组,动态规划,分治算法]
categories: 
- LeetCode
- easy
top:
---

#### 题目描述
给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

<!--more-->

```tex
示例:

输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```
>进阶:
>
如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。

---
#### 建议答案

```java
public int maxSubArray(int[] nums) {
        int nums_size = nums.length;
        int[] max_subarray = new int[nums_size];
        max_subarray[0] = nums[0];
        int max = max_subarray[0];
        for (int i = 1; i < nums_size; i++) {
            max_subarray[i] = Math.max(nums[i], max_subarray[i - 1] + nums[i]);
            max = Math.max(max_subarray[i], max);
        }
        return max;
    }
```

---
#### 思考

##### 1.遍历

```java
 public int maxSubArray(int[] nums) {
        int sum;
        int max = nums[0];
        for (int i = 0; i < nums.length; i++) {
            sum = 0;
            for (int j = i; j < nums.length; j++) {
                max = Math.max(max, sum = nums[j] + sum);
            }
        }
        return max;
    }
    //O(n^2)
```
>显然效率非常低

##### 2.遍历改进

```java
public int maxSubArray(int[] nums) {
        int sum = 0;
        int max = nums[0];
        for (int num : nums) {
//如果sum为正数，不确定下一个元素的符号，则比较下一个元素及sum之和与sum的大小。
            if (sum > 0) {
                sum += num;
            } else {
//如果sum为负数，显然对于下一个元素，加上sum反而更小了,比较上一个sum与下一个元素的大小（上一个元素如果不是最大的，已经被抛弃，如果是最大的则已经被赋值给max）
                sum = num;
            }
            max = Math.max(max, sum);
        }
        return max;
    }
```
>O(n)
>思路巧妙，相当于一遍遍历的时候就弃掉肯定不是答案的那一部分元素

##### 3.动态规划

```java
public int maxSubArray(int[] nums) {
        int nums_size = nums.length;
        int[] max_subarray = new int[nums_size];
        max_subarray[0] = nums[0];
        int max = max_subarray[0];
        for (int i = 1; i < nums_size; i++) {
            max_subarray[i] = Math.max(nums[i], max_subarray[i - 1] + nums[i]);
            max = Math.max(max_subarray[i], max);
        }
        return max;
    }
```
>O(n)
>定义一个函数f(n)，以第n个数为结束点的子数列的最大和，存在一个递推关系f(n) = max(f(n-1) + A[n], A[n]);
将这些最大和保存下来后，取最大的那个就是，最大子数组和。因为最大连续子数组 等价于 最大的以n个数为结束点的子数列和 

##### 4.分治

>分治法的运用条件:
1.原问题可以分解为若干与原问题的解；
2.子问题可以分解并可以求解；
3.子问题的解可以合并为原问题的解；
4.分解后的子问题应互相独立，即不包含重叠子问题（如斐波那契数列）。

太复杂了，不想写