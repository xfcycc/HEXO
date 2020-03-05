---
title: LeetCode066加一
copyright: true
date: 2019-02-25 10:41:05
tags: [数组,数学,LeetCode,算法]
categories: 
- LeetCode
- easy
top:
---

#### 题目描述
给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储一个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

<!--more-->

```tex
示例 1:

输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。
示例 2:

输入: [9]
输出: [1,0]
解释: 输入数组表示数字 10。
```

---
#### 建议答案

>貌似也没有更好的解法

---
#### 思考

##### 自己写的

```java
     public int[] plusOne(int[] nums) {
        if (nums == null) return null;
        int len = nums.length;
        if (nums[len - 1] == 9) {
            for (int i = nums.length - 1; i >= 0; i--) {
                if (nums[i] == 9 && i == 0) {
                    nums[i] = 0;
                    int[] nums2 = new int[len + 1];
                    nums2[0] = 1;
                    System.arraycopy(nums,0,nums2,1,len);
                    return nums2;
                } else if (nums[i] == 9) {
                    nums[i] = 0;
                } else {
                    nums[i] = nums[i] + 1;
                    break;
                }
            }
        } else {
            nums[len - 1] = nums[len - 1] + 1;
            return nums;
        }
        return nums;
    }
```
> 0ms
