---
title: LeetCode001两数之和
copyright: true
date: 2019-02-12 10:42:34
tags: [LeetCode,算法,数组,哈希表]
categories: 
- LeetCode
- easy
top:
---
#### 题目描述:

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。
<!--more-->

示例:

```
给定 nums = [2, 7, 11, 15], target = 9
因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

------

#### 建议答案：

```java
public int[] twoSum(int[] arr,int target)  {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < arr.length; i++) {
            int num = target-arr[i];
            if(map.containsKey(num)){
                return new int []{map.get(num),i};
            }
            map.put(arr[i],i);
        }
        throw new NullPointerException("不存在");
    }
```

------

#### 过程:
第一次看到这个题目的时候还没有学习HashMap，自然的使用的双层for循环来解答，结果超时。
代码如下

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
     int[] h = new int[2];
        sd:for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < nums.length; j++) {
                if (nums[i] + nums[j]==target&&i!=j) {
                    h[0]=i;
                    h[1]=j;
                    break sd;
                }
                else{
                    continue;
                }
            }
        }
        return h;
    }
}
```

看完解答后，知道用HashMap来解答，自写代码如下：

```java
public int[] twoSum(int[] arr,int target)  {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < arr.length; i++) {
            int num = target-arr[i];
            if(map.containsKey(num)){
                return new int []{map.get(num),i};
            }
            map.put(arr[i],i);
        }
        throw new NullPointerException("不存在");
    }

```

------

#### 思考:

1. HashMap的`containskey()`方法时间复杂度是O(1)，如果是最坏结果可能是O(n),因此省下了大量时间，整个算法的时间复杂度是O(n)。
2. HashMap的`containsvalue()`方法可推论，时间复杂度是O(n)。
3. HashMap存储数据用的是哈希表+红黑树。
4. 为了对比红黑树查找的优越性，写了一个ArrayLIst查找方法。
5. `throw new NullPointerException("不存在");`可以代替`return`，也不需要处理（RuntimeException）。

------

#### 对比组：

```java
public static void main(String[] args) {
        Random r = new Random();
        ArrayList<Integer> list = new ArrayList<>();
        for (int i = 0; i < 100000; i++) {   //增加大量元素，为了测试性能，这些元素都不是解
            list.add(r.nextInt(100));
        }
        list.add(1200);
        list.add(125);    //正确解，其他元素都是小于100.

        Object[]arr=list.toArray();  //Object类型，需要强转
        long start = System.currentTimeMillis();
        System.out.println(Arrays.toString(sum(arr,1325)));
        long end = System.currentTimeMillis();
        System.out.println("共耗时毫秒：" + (end-start));
        long start2 = System.currentTimeMillis();
        System.out.println(Arrays.toString(sum2(arr,1325)));
        long end2 = System.currentTimeMillis();
        System.out.println("共耗时毫秒：" + (end2-start2));
    }
    public static int[] sum(Object[] arr,int target)  {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < arr.length; i++) {
            Integer com = target-(int)arr[i];
            if(map.containsKey(com)){
                return new int[]{map.get(com),i};
            }
            map.put((int)arr[i],i);
        }
        throw new NullPointerException("不存在");
    }
    public static int[] sum2 (Object[]arr,int target){
        ArrayList<Integer> list = new ArrayList<>();
        for (int i = 0; i < arr.length; i++) {
            Integer com = target-(int)arr[i];
            if(list.contains(com)){
                return new int[]{list.indexOf(com),i};
            }
            list.add((int)arr[i]);
        }
        throw new NullPointerException("不存在");
    }
```
**结果:**

```
[100000, 100001]
共耗时毫秒：29  
[100000, 100001]
共耗时毫秒：3219
```
差别在方法`map.containskey()`和`list.indexOf()`,两者效率差一个O(n)。

---
#### 总结：
正确的选用数据结构能够提高效率

---
#### MarkDown注意事项：
1. 少量代码使用\`即可，多段代码才用\`\`\`。
2. 行结尾双击空格强制换行(貌似有时候没用，不明)。
3. 语法显示使用\。