---
title: '暑期算法 第十题'
date: 2021-08-18 23:59:59
categories: [算法]
published: true
hideInList: false
feature: 
isTop: false
---


# 题目

给定一个整数数组 `nums` ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

> ```
> 输入：nums = [-2,1,-3,4,-1,2,1,-5,4]
> 输出：6
> 解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。
> ```

> ```
> 输入：nums = [1]
> 输出：1
> ```

> ```
> 输入：nums = [0]
> 输出：0
> ```

> ```
> 输入：nums = [-1]
> 输出：-1
> ```

> ```
> 输入：nums = [-100000]
> 输出：-100000
> ```

来源：LeetCode-53

# 题解

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    let ans = nums[0];
    let sum = 0;
    for(const num of nums) {
        if(sum > 0) {
            sum += num;
        } else {
            sum = num;
        }
        ans = Math.max(ans, sum);
    }
    return ans;
};
```

# 题析

这又又又又是一道动态规划题，难度中等，仍是抓住三个要点：

## 定义数组元素的含义

`dp[i]`：表示以 `nums[i]` **结尾** 的 **连续** 子数组的最大和。

## 找出数组元素间的关系式

根据状态的定义，由于 `nums[i]` 一定会被选取，并且以 `nums[i]` 结尾的连续子数组与以 `nums[i - 1]` 结尾的连续子数组只相差一个元素 `nums[i]` 。

假设数组 `nums` 的值全都严格大于 00，那么一定有 `dp[i] = dp[i - 1] + nums[i]`。

可是 `dp[i - 1]` 有可能是负数，于是分类讨论：

- 如果 `dp[i - 1] > 0`，那么可以把 `nums[i]` 直接接在 `dp[i - 1]` 表示的那个数组的后面，得到和更大的连续子数组；
- 如果 `dp[i - 1] <= 0`，那么 `nums[i]` 加上前面的数 `dp[i - 1]` 以后值不会变大。于是 `dp[i]` 「另起炉灶」，此时单独的一个 `nums[i]` 的值，就是 `dp[i]`。

综上可以推导出```dp[i]=max{nums[i] , dp[i−1]+nums[i]}```。

## 找出初始条件

`dp[0] = nums[0]`

# 题外

又是一道凭空想不出解的动态规划题，还是得多刷几道才行。