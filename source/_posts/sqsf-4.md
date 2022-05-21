---
title: '暑期算法 第四题'
date: 2021-08-12 23:43:45
categories: [算法]
published: true
hideInList: false
feature: 
isTop: false
---
# 题目

给定一个 *n* × *n* 的二维矩阵 `matrix` 表示一个图像。请你将图像顺时针旋转 90 度。

你必须在**原地**旋转图像，这意味着你需要直接修改输入的二维矩阵。请**不要**使用另一个矩阵来旋转图像。

> ![](https://assets.leetcode.com/uploads/2020/08/28/mat1.jpg)
>
> ```
> 输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
> 输出：[[7,4,1],[8,5,2],[9,6,3]]
> ```

> ![](https://assets.leetcode.com/uploads/2020/08/28/mat2.jpg)
>
> ```
> 输入：matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]
> 输出：[[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]
> ```

> ```
> 输入：matrix = [[1]]
> 输出：[[1]]
> ```

> ```
> 输入：matrix = [[1,2],[3,4]]
> 输出：[[3,1],[4,2]]
> ```


来源：LeetCodeHOT100-48

# 题解

```javascript
var rotate = function(matrix) {
    const n = matrix.length;
    // 左右翻转
    for (let i = 0; i < Math.floor(n / 2); i++) {
        for (let j = 0; j < n; j++) {
            [matrix[i][j], matrix[n - i - 1][j]] = [matrix[n - i - 1][j], matrix[i][j]];
        }
    }
    // 矩阵转置
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < i; j++) {
            [matrix[i][j], matrix[j][i]] = [matrix[j][i], matrix[i][j]];
        }
    }
};
```

# 题析

转置矩阵：将矩阵的行和列调换，也可理解为主对角线翻转。

![转置矩阵](https://i.loli.net/2021/08/12/m5GV2qfeK819cDz.png)

题目顺时针旋转90°可以看做将矩阵左右翻转+矩阵转置。

# 题外

通过左右翻转、上下翻转和矩阵转置，可以实现矩阵的任意旋转。

- 顺时针180°：上下翻转+左右翻转
- 顺时针270°：上下翻转+矩阵转置

```javascript
// 左右翻转
for (let i = 0; i < Math.floor(n / 2); i++) {
  for (let j = 0; j < n; j++) {
    [matrix[i][j], matrix[n - i - 1][j]] = [matrix[n - i - 1][j], matrix[i][j]];
  }
}
// 上下翻转
for (let i = 0; i < Math.floor(n / 2); i++) {
    for (let j = 0; j < n; j++) {
        [matrix[j][i], matrix[j][n - i - 1]] = [matrix[j][n - i - 1], matrix[j][i]];
    }
}
// 矩阵转置
for (let i = 0; i < n; i++) {
  for (let j = 0; j < i; j++) {
    [matrix[i][j], matrix[j][i]] = [matrix[j][i], matrix[i][j]];
  }
}
```

