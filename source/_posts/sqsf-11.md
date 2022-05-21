---
title: '暑期算法 第十一题'
date: 2021-08-23 23:58:51
categories: [算法]
published: true
hideInList: false
feature: 
isTop: false
---
# 题目

给你一个整数数组 `nums` ，找到其中最长严格递增子序列的长度。

子序列是由数组派生而来的序列，删除（或不删除）数组中的元素而不改变其余元素的顺序。例如，`[3,6,2,7]` 是数组 `[0,3,1,6,2,2,7]` 的子序列。

> ```
> 输入：nums = [10,9,2,5,3,7,101,18]
> 输出：4
> 解释：最长递增子序列是 [2,3,7,101]，因此长度为 4 。
> ```

> ```
> 输入：nums = [0,1,0,3,2,3]
> 输出：4
> ```

> ```
> 输入：nums = [7,7,7,7,7,7,7]
> 输出：1
> ```

来源：LeetCode-300

# 题解

```javascript
const lengthOfLIS = (nums) => {
    let dp = Array(nums.length).fill(1);
    let result = 1;

    for(let i = 1; i < nums.length; i++) {
        for(let j = 0; j < i; j++) {
            if(nums[i] > nums[j]) {
                dp[i] = Math.max(dp[i], dp[j]+1);
            }
        }
        result = Math.max(result, dp[i]);
    }

    return result;
};
```

# 题析

这又<sup>5</sup>是一道动态规划题，是子序列系列问题的入门题，仍是抓住三个要点：

## 定义数组元素的含义

`dp[i]`：考虑前 *i* 个元素，以第 *i* 个数字结尾的最长上升子序列的长度。

需要把第 *i* 个元素考虑进去，即假设`nums=[1,2,3]`，`dp[2]`表示从下标0到下标2的最长上升子序列，很显然等于3。

## 找出数组元素间的关系式

`dp[i] = max(dp[j])+1`，其中`0 ≤ j < i`且`num[j] < num[i]`

参考力扣[官方解析](https://leetcode-cn.com/problems/longest-increasing-subsequence/solution/zui-chang-shang-sheng-zi-xu-lie-by-leetcode-soluti/)中的动画演示能更好理解。

需要二层循环，外层假设`nums[i]`为子序列的最后一个元素，内层假设`nums[j]`为子序列的第一个元素，结合`dp[i]`的定义，就能得到最长度。

时间复杂度是O(n<sup>2</sup>)。

## 找出初始条件

`dp[1] = 1`

# 题外

虽然是入门子序列的问题，但对我而言仍是秃头难想得出的，理解答案已经有点难了，还需要不断的记忆相关类型的套路才行。