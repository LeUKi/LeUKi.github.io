---
title: '暑期算法 第七题'
date: 2021-08-15 23:59:59
categories: [算法]
published: true
hideInList: false
feature: 
isTop: false
---
# 题目

一个机器人位于一个 `m x n` 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish” ）。

问总共有多少条不同的路径？

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

> ```
> 输入：m = 3, n = 7
> 输出：28
> ```

> ```
> 输入：m = 3, n = 2
> 输出：3
> 解释：
> 从左上角开始，总共有 3 条路径可以到达右下角。
> 1. 向右 -> 向下 -> 向下
> 2. 向下 -> 向下 -> 向右
> 3. 向下 -> 向右 -> 向下
> ```

> ```
> 输入：m = 7, n = 3
> 输出：28
> ```

> ```
> 输入：m = 3, n = 3
> 输出：6
> ```

来源：LeetCodeHOT100-62

# 题解

```javascript
var uniquePaths = function(m, n) {
    const f = new Array(m).fill(0).map(() => new Array(n).fill(0));
    for (let i = 0; i < m; i++) {
        f[i][0] = 1;
    }
    for (let j = 0; j < n; j++) {
        f[0][j] = 1;
    }
    for (let i = 1; i < m; i++) {
        for (let j = 1; j < n; j++) {
            f[i][j] = f[i - 1][j] + f[i][j - 1];
        }
    }
    return f[m - 1][n - 1];
};
```

# 题析

这又是一道动态规划题，继续抓住三个要点：

## 定义数组元素的含义

定义 `dp[i][j]` 的含义为：从左上角走到 (*i*,*j*) 的路径数量。

## 找出数组元素间的关系式

到达(i,j)有两种方式：

- 一种是从上往下

- 一种是从左往右

算所有可能的路径，所以有 `dp[i，j] = dp[i-1][j] + dp[i][j-1]`。

## 找出初始条件

`dp[0][0]`、`dp[0][j]`、`dp[i][0]`都为1。

# 题外

这是一道很基础的二维动态规划题，与一维的思想是相似的，二维动态规划是在寻找`dp[i][j]`与`dp[i-1][j]`、`dp[i][j-1]`、`dp[i-1][j-1]`的关系。

