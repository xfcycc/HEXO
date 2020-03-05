---
title: LeetCode118杨辉三角
copyright: true
date: 2019-02-25 20:45:29
tags: [LeetCode,算法,数组,二维数组]
categories: 
- LeetCode
- easy
top:
---
#### 题目描述
给定一个非负整数 numRows，生成杨辉三角的前 numRows 行。

在杨辉三角中，每个数是它左上方和右上方的数的和。
<!--more-->
```tex
示例:

输入: 5
输出:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

---
#### 建议答案

````java
 public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> lists = new ArrayList<>();
        int[][] arr = new int[numRows][numRows];
        for (int i = 0; i < numRows; i++) {
            List<Integer> list = new ArrayList<>();
            for (int j = 0; j <= i; j++) {
                if (j == 0) {
                    arr[i][j] = 1;
                } else if (j == i) {
                    arr[i][j] = 1;
                } else {
                    arr[i][j] = arr[i - 1][j - 1] + arr[i - 1][j];
                }
                list.add(arr[i][j]);
            }
            lists.add(list);
        }
        return lists;
    }
````

---
#### 思考

##### 二维数组遍历

```java
 public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> lists = new ArrayList<>();
        int[][] arr = new int[numRows][numRows];
        for (int i = 0; i < numRows; i++) {
            List<Integer> list = new ArrayList<>();
            for (int j = 0; j <= i; j++) {
                if (j == 0) {
                    arr[i][j] = 1;    //杨辉三角每一行开头结尾都是1
                } else if (j == i) {
                    arr[i][j] = 1;
                } else {
                    arr[i][j] = arr[i - 1][j - 1] + arr[i - 1][j];
                }
                list.add(arr[i][j]);
            }
            lists.add(list);
        }
        return lists;
    }
```
