---
title: LeetCode020有效的括号
copyright: true
date: 2019-02-16 12:56:23
tags: [LeetCode,算法,栈,字符串]
categories: 
- LeetCode
- easy
top:
---
#### 题目描述：
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。

左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。

<!--more-->
```tex
示例 1:

输入: "()"
输出: true

示例 2:

输入: "()[]{}"
输出: true

示例 3:

输入: "(]"
输出: false

示例 4:

输入: "([)]"
输出: false

示例 5:

输入: "{[]}"
输出: true

```

---
#### 建议答案：

```java
public boolean isValid(String s) {
    //击败35%的速度
        if (s.length() == 0) return true;
        HashMap map = new HashMap<Character, Character>();
        map.put(']', '[');
        map.put('}', '{');
        map.put(')', '(');
        Stack<Character> stk = new Stack<>();
        char[] chars = s.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            if (map.containsKey(chars[i])) {
                if (stk.empty() ||stk.peek()!=(map.get(chars[i])) {
                    return false;  //当出现右括号的时候栈空或者栈顶不匹配，字符串无效
                } else {
                    stk.pop(); //匹配，弹栈
                }
            } else {
                stk.push(chars[i]);//出现左括号，正常推栈
            }

        }
        return stk.empty();
        }
    }
```

---
#### 思考：
```tex
() [] {}
{[([])]}

1. 当出现左括号，推栈
2. 当出现右括号，判断栈顶是否匹配，如果栈为空或者不匹配，字符串无效
3. 最后栈不为空，字符串无效
```

```java
public boolean isValid(String s) {
    //击败35%的速度
        if (s.length() == 0) return true;
        HashMap map = new HashMap<Character, Character>();
        map.put(']', '[');
        map.put('}', '{');
        map.put(')', '(');
        Stack<Character> stk = new Stack<>();
        char[] chars = s.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            if (map.containsKey(chars[i])) {
                if (stk.empty() ||stk.peek()!=(map.get(chars[i])) {
                    return false;  //当出现右括号的时候栈空或者栈顶不匹配，字符串无效
                } else {
                    stk.pop(); //匹配，弹栈
                }
            } else {
                stk.push(chars[i]);//出现左括号，正常推栈
            }

        }
        return stk.empty();
        }
    }
```
> O(n)

---
#### 总结：

1. 算法基础不够了，需要补基础。

2. 只要能实现算法，优化是迟早的事。

3. 很多的判断语句可以转化为哈希表查找。 