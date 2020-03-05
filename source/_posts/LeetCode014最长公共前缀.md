---
title: LeetCode014最长公共前缀
copyright: true
date: 2019-02-14 18:58:07
tags: [LeetCode,算法,字符串]
categories: 
- LeetCode
- easy
top:
---

#### 题目描述：
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。
<!--more-->

```tex
示例 1:

输入: ["flower","flow","flight"]
输出: "fl"

示例 2:

输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
```

>说明:
所有输入只包含小写字母 a-z 。

---
#### 建议答案：

```java
public String longestCommonPrefix(String[] strs) {
        String str = "";
        if (strs.length > 0) {
            str = strs[0];
            for (int i = 1; i < strs.length; i++) {
                while (!strs[i].startsWith(str)) {
                    if (str.length() > 1) {
                        str = str.substring(0, str.length() - 1);
                    } else {
                        return "";
                    }
                }
            }
        }
        return str;
    }       
```

---
#### 思考：

##### 1. 暴力遍历:

1. 找出最短的元素
2. 遍历这个元素的字符，将第一个字符与所有元素比较
3. 相同就继续，如果都不相同就返回空字符串
4. 继续遍历，直到有不相同的

```java
//执行用时: 11 ms, 在Longest Common Prefix的Java提交中击败了57.60% 的用户
//内存消耗: 23.8 MB, 在Longest Common Prefix的Java提交中击败了91.09% 的用户
public String longestCommonPrefix(String[] arr) {
        if (arr.length == 0) return "";
        if (arr.length == 1) return arr[0];
        String s = "";
        int index = 0;
        for (int i = 0; i < arr.length; i++) {
            if (arr[i].length() <= arr[index].length()) index = i;
        }
        char chars[] = arr[index].toCharArray();
        for (int i = 0; i < chars.length; i++) {
            for (int j = 0; j < arr.length; j++) {
                if (chars[i] != arr[j].charAt(i)) {
                    return s;
                }
            }
            s += chars[i];
        }
        return s;
    }
```

##### 2.递归：
1. 定义算法LCP，寻找两个字符串的最长公共前缀。
2. 利用算法LCP遍历数组。


```java
 //28 ms ,击败5%，太慢了
 public static String longestCommonPrefix(String[] arr) {
        if (arr.length == 1) {
            return arr[0];
        }
        if (arr.length == 0) return "";
        String sWith = arr[0];
        for (
                int i = 0;
                i < arr.length - 1; i++) {
            sWith = LCP(sWith, arr[i + 1]);
        }
        return sWith;
    }

    public static String LCP(String s1, String s2) {
        String s = "";
        int length = Math.min(s1.length(), s2.length());
        for (int i = 0; i < length; i++) {
            if (s1.charAt(i) == s2.charAt(i)) {
                s += s1.charAt(i);
            } else {
                return s;
            }
        }
        return s;
    }
```
>一般情况下最常用的，虽然很慢

#### LeetCode提交记录里最快的：

```java
//执行用时: 5 ms, 在Longest Common Prefix的Java提交中击败了99.97% 的用户
//内存消耗: 27.1 MB, 在Longest Common Prefix的Java提交中击败了40.11% 的用户
public String longestCommonPrefix(String[] strs) {
        String str = "";
        if (strs.length > 0) {
            str = strs[0];
            for (int i = 1; i < strs.length; i++) {
                while (!strs[i].startsWith(str)) {
                    if (str.length() > 1) {
                        str = str.substring(0, str.length() - 1);
                    } else {
                        return "";
                    }
                }

            }
        }
        return str;
    }       
```

> 太厉害了,一边遍历
