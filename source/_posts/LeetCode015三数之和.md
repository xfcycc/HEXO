---
title: LeetCode015三数之和
copyright: true
date: 2019-03-05 13:04:16
tags: [数组,双指针,LeetCode,算法]
categories: 
- LeetCode
- medium
top:
---

#### 题目描述
给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

<!--more-->

```tex
例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

---
#### 建议答案

```java
   public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums);
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > 0) break;
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            int j = nums.length - 1;
            int target = 0 - nums[i];
            int k = i + 1;
            while (k < j) {
                if (nums[k] + nums[j] == target) {
                    List<Integer> item = Arrays.asList(nums[i], nums[k], nums[j]);
                    result.add(item);
                    while (k < j && nums[k] == nums[k + 1]) k++;
                    while (k < j && nums[j] == nums[j - 1]) j--;
                    k++;j--;
                } else if (nums[k] + nums[j] < target) {
                    k++;
                } else {
                    j--;
                }
            }
        }
        return result;
    }
```
#### 思考
##### 1
一开始的思路是先取出一个，剩下的两个数转为两数之和

```java
 public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> arrayLists = new ArrayList<>();
        HashSet<List<Integer>> set = new HashSet<>();
        Arrays.sort(nums); // -4,-1,-1,0,1,2,如果不排序会出现重复结果
        for (int i = 0; i < nums.length-2; i++) {
            HashMap<Integer, Integer> map = new HashMap<>();
            int target = 0 - nums[i];
            for (int j = i + 1; j < nums.length; j++) {
                if (map.containsKey(target - nums[j])) {
                   set.add(Arrays.asList(nums[j], nums[i], nums[map.get(target - nums[j])]));
                } else {
                    map.put(nums[j], j);
                }
            }
        }
        for (List<Integer> integers : set) {
            arrayLists.add(integers);
        }
        return arrayLists;
    }
```
时间复杂度太高了，不过一次过也是不容易。。。。用时1000ms

##### 2
LeetCode有如下解答

```java
 public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> ls = new ArrayList<>();
 
        for (int i = 0; i < nums.length - 2; i++) {
            if (i == 0 || (i > 0 && nums[i] != nums[i - 1])) {  // 跳过可能重复的答案
 
                int l = i + 1, r = nums.length - 1, sum = 0 - nums[i];
                while (l < r) {
                    if (nums[l] + nums[r] == sum) {
                        ls.add(Arrays.asList(nums[i], nums[l], nums[r]));
                        while (l < r && nums[l] == nums[l + 1]) l++;
                        while (l < r && nums[r] == nums[r - 1]) r--;
                        l++;
                        r--;
                    } else if (nums[l] + nums[r] < sum) {
                        while (l < r && nums[l] == nums[l + 1]) l++;   // 跳过重复值
                        l++;
                    } else {
                        while (l < r && nums[r] == nums[r - 1]) r--;
                        r--;
                    }
                }
            }
        }
        return ls;
    }
```
>100ms
##### 3

```java
public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums);
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > 0) break;
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            int j = nums.length - 1;
            int target = 0 - nums[i];
            int k = i + 1;
            while (k < j) {
                if (nums[k] + nums[j] == target) {
                    List<Integer> item = Arrays.asList(nums[i], nums[k], nums[j]);
                    result.add(item);
                    while (k < j && nums[k] == nums[k + 1]) k++;
                    while (k < j && nums[j] == nums[j - 1]) j--;
                    k++;j--;
                } else if (nums[k] + nums[j] < target) {
                    k++;
                } else {
                    j--;
                }
            }
        }
        return result;
    }
```
>80ms