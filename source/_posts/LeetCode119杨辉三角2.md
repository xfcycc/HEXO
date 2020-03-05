---
title: LeetCode119杨辉三角2
copyright: true
date: 2019-02-25 21:01:28
tags: [LeetCode,算法,数组]
categories:
- LeetCode
- easy
top:
---

#### 题目描述
给定一个非负索引 k，其中 k ≤ 33，返回杨辉三角的第 k 行。

在杨辉三角中，每个数是它左上方和右上方的数的和。

<!--more-->
```tex
示例:

输入: 3
输出: [1,3,3,1]
```

>进阶：
你可以优化你的算法到 O(k) 空间复杂度吗？

---
#### 建议答案

```java
 public List<Integer> getRow(int rowIndex) {
        List<Integer> res = new ArrayList<Integer>();
        long nk = 1;
        for (int i = 0; i <= rowIndex; i++) {
            res.add((int) nk);
            nk = nk * (rowIndex - i) / (i + 1);
        }
        return res;
    }
```

>数学公式，背就完事了
>空间复杂度为O(k)

#### 思考
如果是我的话，就把上一题代码拿出来，输出就完事。