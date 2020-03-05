---
title: LeetCode007整数反转
copyright: true
date: 2019-02-13 12:23:33
tags: [LeetCode,算法,数学]
categories: 
- LeetCode
- easy
top:
---
#### 题目描述：
给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

<!--more-->

```tex
示例 1:

输入: 123
输出: 321

示例 2:

输入: -123
输出: -321

示例 3:

输入: 120
输出: 21
```
>注意:
>
>假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−2^31,  2^31 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。



---
#### 建议答案：

```java
 public int reverse(int x) {
        int ret = 0;
        while(x != 0) {
            int temp = ret*10 + x%10;
            if(temp / 10 != ret)
                return 0;
            ret = temp;
            x /= 10;
        }
        return ret;
    }
```

---

#### 思考：

在不考虑取值范围的情况下，可以轻松得出以下解：

```java
public int reverse(int i) {
        int temp = 0;
        while (i != 0) {
            int pop = i % 10;
            i /= 10;
            temp = temp * 10 + pop;
        }
        return temp;
    }
```

32位有符号`int`类型范围是[−2^31,  2^31 − 1]，即[-2147483648,2147483647]。

因为参数限制为`int`类型，因此不用判断输入的数字是否溢出内，但是要确保反转的数字不会溢出，溢出则返回零。

观察代码，只有这一句`temp = temp * 10 + pop`可能导致溢出，且后面的代码直接输出了`temp`，因此要在这句代码执行之前就判断执行这段代码之后是否会溢出,即在`i /= 10`之后。

为了书写方便，用`max`代替向上取值范围，`min`代替向下取值范围。

先判断向上的范围，显然，如果`temp > max / 10`,则结果必定会溢出。

如果`temp = max / 10`呢，由于`int`运算后会舍弃溢出部分，如`max / 10 == 214748364 == temp`,显然`temp`没有溢出，那么就要考虑`pop`了。显然，pop在小于等于7的时候，不会溢出。

即代码：

```java
if (temp > Integer.MAX_VALUE / 10 || (temp == Integer.MAX_VALUE / 10 && pop > 7)) return 0;
```

向下同理：

```java
if (temp < Integer.MIN_VALUE / 10 || (temp == Integer.MIN_VALUE / 10 && pop < -8)) return 0;
```

最终代码：

```java
public static int reverse(int i) {
        int temp = 0;
        while (i != 0) {
            int pop = i % 10;
            i /= 10;
            if (temp > Integer.MAX_VALUE / 10 || (temp == Integer.MAX_VALUE / 10 && pop > 7)) return 0;
            if (temp < Integer.MIN_VALUE / 10 || (temp == Integer.MIN_VALUE / 10 && pop < -8)) return 0;
            temp = temp * 10 + pop;
        }
        return temp;
    }
```

---
#### 参考答案：
  ##### 1.官方答案：

```java
class Solution {
    public int reverse(int x) {
        int rev = 0;
        while (x != 0) {
            int pop = x % 10;
            x /= 10;
            if (rev > Integer.MAX_VALUE/10 || (rev == Integer.MAX_VALUE / 10 && pop > 7)) return 0;
            if (rev < Integer.MIN_VALUE/10 || (rev == Integer.MIN_VALUE / 10 && pop < -8)) return 0;
            rev = rev * 10 + pop;
        }
        return rev;
    }
}
```
>Integer.MAX_VALUE : 2147483647 , Integer.MIN_VALUE : -2147483648

##### 2.参考答案：

```java
 public int reverse(int x) {
        int ret = 0;
        while(x != 0) {
            int temp = ret*10 + x%10;
            if(temp / 10 != ret)
                return 0;
            ret = temp;
            x /= 10;
        }
        return ret;
    }
```

拆解开来，如果不判断溢出，则

```java
int ret = ret*10 + x %10;
x /= 10;
```

这段代码本质上和第一段代码没有区别。

这个答案利用temp来判断是否溢出，则

```java
int temp = ret * 10 + x % 10;

ret = temp;
x /= 10;
```

空出的一行就是判断代码，显而易见，如果temp溢出，结果会变得不可知,再除以10以去掉x加上的尾数显然无法得到原来的ret。

如，x取1234567899，最后一步会变成这样：

```java
 public int reverse(int x) {
        int ret = 0;
        while(x != 0) {
            int temp = ret*10 + x%10; //此时ret = 998765432 ， x = 1
            if(temp / 10 != ret)      //下一步temp = 1397719729(溢出)
                return 0;
            ret = temp;
            x /= 10;
        }
        return ret;
    }
```

---
#### 总结：
1. 考虑算法逻辑需要一步一步来。