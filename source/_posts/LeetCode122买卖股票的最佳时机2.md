---
title: LeetCode122买卖股票的最佳时机2
copyright: true
date: 2019-02-26 14:29:10
tags: [贪心算法,数组,LeetCode,算法]
categories: 
- LeetCode
- easy
top:
---

####  题目描述
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

<!--more-->
注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

```tex
示例 1:

输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
示例 2:

输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
示例 3:

输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

---
#### 建议答案

```java
  public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) {
            return 0;
        }
        int max = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                max += prices[i] - prices[i - 1];
            }
        }
        return max;
```

---
#### 思考
##### 贪心算法

>贪心算法要求使用前证明
>在涨价的前一天卖出，在降价的前一天买入
>进一步简化，只要有差值就可以买卖

```java
 public static int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) {
            return 0;
        }
        int max = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                max += prices[i] - prices[i - 1];
            }
        }
        return max;
```

>1. 如果有一个低价格，后面连续波动直到达到最高，那么从这个低价格开始，后面每天的差值加起来等于低价格和高价格直接的差值。
>2. 如果是高低价格，直接低价买入，高价卖出即可。