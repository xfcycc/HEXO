---
title: LeetCode169求众数
copyright: true
date: 2019-03-03 19:00:49
tags: [位运算,数组,分治算法,LeetCode,算法]
categories: 
- LeetCode
- easy
top:
---

#### 题目描述
给定一个大小为 n 的数组，找到其中的众数。众数是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在众数。

<!--more-->

```tex
示例 1:

输入: [3,2,3]
输出: 3

示例 2:

输入: [2,2,1,1,1,2,2]
输出: 2
```

---
#### 建议答案

```java
public int majorityElement(int[] nums) {
        int ele = nums[0];
        int cout = 1;
        for (int num : nums) {
            if (num == ele) {
                cout++;
            } else {
                cout--;
                if (cout == 0) {
                    cout ++;
                    ele = num;
                }
            }

        }
        return ele;
    }
```

---
#### 思考

##### 1.遍历解法

```java
 public int majorityElement(int[] nums) {
        int ele = nums[0];
        int cout = 1;
        for (int i = 1; i < nums.length - 1; i++) {
            if (nums[i] == ele) {
                cout++;
            } else {
                cout--;
                if (cout == 0) {
                    ele = nums[i++ + 1];
                    cout++;
                }
            }

        }
        return ele;
    }
```

>遍历，从第一个数开始，计数器记为1，遇到相同的加一，遇到不同的减一，如果为0就换一个数
>O(n)


##### 2.骚操作

```java
public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length / 2];
    }
```


