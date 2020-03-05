---
title: LeetCode013罗马数字转整数
copyright: true
date: 2019-02-14 12:39:33
tags: [LeetCode,算法,数学,字符串]
categories:
- LeetCode
- easy
top:
---
####  题目描述：

罗马数字包含以下七种字符:` I`，` V`， `X`，` L`，`C`，`D` 和` M`。

```tex
字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

例如， 罗马数字 2 写做 `II` ，即为两个并列的 1。12 写做` XII` ，即为` X` +` II` 。 27 写做  `XXVII`, 即为`XX` +`V` +` II` 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做` IIII`，而是 `IV`。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为` IX`。这个特殊的规则只适用于以下六种情况：

`I` 可以放在 `V` (5) 和 `X` (10) 的左边，来表示 4 和 9。
`X` 可以放在 `L` (50) 和 `C` (100) 的左边，来表示 40 和 90。 
`C` 可以放在 `D` (500) 和 `M` (1000) 的左边，来表示 400 和 900。
给定一个罗马数字，将其转换成整数。输入确保在 1 到 3999 的范围内。

<!--more-->

```
示例 1:

输入: "III"
输出: 3

示例 2:

输入: "IV"
输出: 4

示例 3:

输入: "IX"
输出: 9

示例 4:

输入: "LVIII"
输出: 58
解释: L = 50, V= 5, III = 3.

示例 5:

输入: "MCMXCIV"
输出: 1994
解释: M = 1000, CM = 900, XC = 90, IV = 4.
```
> 额外的,用于检验代码正确性：输入“MCDLXXVI”,输出1476

---
#### 建议答案：

```java
public int romanToInt(String s) {
//        执行用时: 63 ms, 在Roman to Integer的Java提交中击败了87.86% 的用户
//        内存消耗: 24.2 MB, 在Roman to Integer的Java提交中击败了87.63% 的用户
        HashMap<Character, Integer> map = new HashMap<>();
        int sum = 0;
        map.put('I', 1);
        map.put('V', 5);
        map.put('X', 10);
        map.put('L', 50);
        map.put('C', 100);
        map.put('D', 500);
        map.put('M', 1000);
        //从后向前遍历
        for (int i = s.length() - 1; i >= 0; i--) { 
        //第一个条件是遍历到最后一个字符串时，由于没有左边的字符串了，直接输出。第二个条件是当字符串长度为1时，直接输出，
            if (i == 0 || s.length() == 1) {
                return sum += map.get(s.charAt(0));
            } else if (map.get(s.charAt(i)) <= map.get(s.charAt(i - 1))) {
                sum += map.get(s.charAt(i));
            } else if (map.get(s.charAt(i)) > map.get(s.charAt(i - 1))) {
                sum += map.get(s.charAt(i)) - map.get(s.charAt(i - 1));
        //这里直接操作了两个字符，因此要再i--;
                i--;
            }
        }
        return sum;
    }
```

---
#### 思考：

考虑使用`HashMap`来存储字符和数字对应。

对于罗马数字字符串,将每一个字符提取出来匹配`HashMap`中的值，再结合起来即可，可以用`ChatAt()或者toCharArray()`。

对于算法：

1. 从后向前遍历，（通常情况下左边大于等于右边） 54321。
2. 如果右边大于左边，则是特殊情况。
3. 那么，当右边小于等于向左的一位时，加上，大于的时候，减去。
4. 注意临界条件，如最后一位。

---
#### 答案：

```java
public int romanToInt(String s) {
//        执行用时: 63 ms, 在Roman to Integer的Java提交中击败了87.86% 的用户
//        内存消耗: 24.2 MB, 在Roman to Integer的Java提交中击败了87.63% 的用户
        HashMap<Character, Integer> map = new HashMap<>();
        int sum = 0;
        map.put('I', 1);
        map.put('V', 5);
        map.put('X', 10);
        map.put('L', 50);
        map.put('C', 100);
        map.put('D', 500);
        map.put('M', 1000);
        //从后向前遍历
        for (int i = s.length() - 1; i >= 0; i--) { 
        //第一个条件是遍历到最后一个字符串时，由于没有左边的字符串了，直接输出。第二个条件是当字符串长度为1时，直接输出，
            if (i == 0 || s.length() == 1) {
                return sum += map.get(s.charAt(0));
            } else if (map.get(s.charAt(i)) <= map.get(s.charAt(i - 1))) {
                sum += map.get(s.charAt(i));
            } else if (map.get(s.charAt(i)) > map.get(s.charAt(i - 1))) {
                sum += map.get(s.charAt(i)) - map.get(s.charAt(i - 1));
        //这里直接操作了两个字符，因此要再i--;
                i--;
            }
        }
        return sum;
    }
```
> 考虑到数组查找比字符串快，可以转换成数组查找

```java
public int romanToInt(String s) {
//      执行用时: 54 ms, 在Roman to Integer的Java提交中击败了93.02% 的用户
//      内存消耗: 28.4 MB, 在Roman to Integer的Java提交中击败了67.78% 的用户
        HashMap<Character, Integer> map = new HashMap<>();
        int sum = 0;
        map.put('I', 1);
        map.put('V', 5);
        map.put('X', 10);
        map.put('L', 50);
        map.put('C', 100);
        map.put('D', 500);
        map.put('M', 1000);
        char[] chars = s.toCharArray();
        for (int i = s.length() - 1; i >= 0; i--) {
            if (i == 0 || s.length() == 1) {
                return sum += map.get(s.charAt(0));
            } else if (map.get(chars[i]) <= map.get(chars[i - 1])) {
                sum += map.get(chars[i]);
            } else if (map.get(chars[i]) > map.get(chars[i - 1])) {
                sum += map.get(chars[i]) - map.get(chars[i - 1]);
                i--;
            }
        }

        return sum;
    }
```

---
#### 总结：
1. 认真读题，按步骤写下来算法，再实现。
2. 空间和时间可以互相转换。
   