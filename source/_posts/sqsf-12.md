---
title: '暑期算法 第十二题'
date: 2021-08-28 01:10:50
categories: [算法]
published: true
hideInList: false
feature: 
isTop: false
---
# 题目

给定一个未经排序的整数数组，找到最长且 连续递增的子序列，并返回该序列的长度。

连续递增的子序列 可以由两个下标` l` 和 `r`（l < r）确定，如果对于每个 `l <= i < r`，都有 `nums[i] < nums[i + 1]` ，那么子序列 `[nums[l], nums[l + 1], ..., nums[r - 1], nums[r]]` 就是连续递增子序列。

> ```
> 输入：nums = [1,3,5,4,7]
> 输出：3
> 解释：最长连续递增序列是 [1,3,5], 长度为3。
> 尽管 [1,3,5,7] 也是升序的子序列, 但它不是连续的，因为 5 和 7 在原数组里被 4 隔开。 
> ```

> ```
> 输入：nums = [2,2,2,2,2]
> 输出：1
> 解释：最长连续递增序列是 [2], 长度为1。
> ```

来源：LeetCode-674

# 题解

```javascript
onst findLengthOfLCIS = nums => {
    const len = nums.length;
    if (len === 1) return 1;
    let res = 1;
    const dp = new Array(len).fill(1);
    for (let i = 1; i < len; i++) {
        if (nums[i] > nums[i - 1]) {
            dp[i] = dp[i - 1] + 1;
        }
        // 更新最大长度
        res = dp[i] > res ? dp[i] : res;
    }
    return res;
};
```

# 题析

这又<sup>6</sup>是一道动态规划题，也能用贪心解决，是道水题，这里主要展现动态规划思想，仍是三部曲：

## 定义数组元素的含义

`dp[i]`：从0到下标为i的子数组中，最后一个连续递增序列的长度。

## 找出数组元素间的关系式

若`nums[i] > nums[i - 1]`，则`dp[i] = dp[i - 1] + 1`。



## 找出初始条件

`dp[0] = 1`

# 题外

用贪心会更好，但结合动态规划会有更好的理解。dp的定义需要巧妙的构思，需要抓住`dp[i]`与`i`的关系，这里应该有想法出来但我写不出文字。

