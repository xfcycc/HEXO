---
title: LeetCode009回文数
copyright: true
date: 2019-02-13 18:59:12
tags: [LeetCode,算法,数学]
categories: 
- LeetCode
- easy
top:
---
#### 题目描述：
判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

<!--more-->
```tex
示例 1:

输入: 121
输出: true

示例 2:

输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。

示例 3:

输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
```
>**进阶：**
你能不将整数转为字符串来解决这个问题吗？

---
#### 建议答案：

```java
 public boolean isPalindrome(int x) {
        if (x < 0 || (x % 10 == 0 && x != 0)) {
            return false;
        }
        int revertedNum = 0;
        while (x > revertedNum) {
            revertedNum = revertedNum * 10 + x % 10;
            x /= 10;
        }
        return (x == revertedNum || x == revertedNum / 10);
    }
```

---
#### 思考：

先用字符串试试：

```java
public boolean isPalindrome(Integer i) {
        String str = i.toString();
        String strExchange = "";
        for (int j = str.length() - 1; j >= 0; j--) {
            strExchange += str.charAt(j);
        }
        if (strExchange.equals(str)) {
            return true;
        } else {
            return false;
        }
    }
```
首先，所有负数pass。

反转所有位上的数字即可,可以用之前的整数反转算法：

```java
 public boolean isPalindrome(int i) {
        if (i < 0) return false;
        int ret = 0;
        int temp = i;
        while (i != 0) {
            ret = ret * 10 + i % 10;
            i /= 10;
        }
        if (temp == ret) {
            return true;
        } else {
            return false;
        }
    }
```

如果担心溢出，改为`long`类型即可。

但是这样不严谨，毕竟有溢出，那么如果是反转一半数字呢？只要反转的一半数字与另一半相同，即可认定是回文数。

怎样知道已经反转到一半了呢？因为反转后的数字`revertedNum`不断乘10，原数字`x`不断除以10，显而易见，当反转后得到的新数`revertedNum`大于反转后的原数字`x`的时候，就是反转到一半了。

当原数字为偶数时，此时原数字和反转后的数字判断相等即可，反转条件需要两个数字不相等，且反转后的数大于原数字，综合起来就是当原数字大于反转后的数时候一直反转。

当原数字为奇数时，最后会得到不等的数字，根据判断条件可知反转后的数字比原数字此时要多一位，多出的一位就是中间那一位，除以10去掉即可，不影响判断。

---
#### 答案：

```java
 public boolean isPalindrome(int x) {
        if (x < 0 || (x % 10 == 0 && x != 0)) {
            return false;
        }
        int revertedNum = 0;
        while (x > revertedNum) {
            revertedNum = revertedNum * 10 + x % 10;
            x /= 10;
        }
        return (x == revertedNum || x == revertedNum / 10);
    }
```

---
#### 总结：
1. 整数反转真好用。
2. 返回语句可以代替许多if语句
