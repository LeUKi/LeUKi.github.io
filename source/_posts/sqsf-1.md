---
title: '暑期算法 第一题'
date: 2021-08-09 22:36:19
categories: [算法]
published: true
hideInList: false
feature: 
isTop: false
---
# 题目

求 1+2+...+n ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）

来源：剑指offer 64

# 题解

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var sumNums = function(n) {
    var flag = n > 1 && (n += sumNums(n - 1)) > 0
    return n;
};
```

# 题析

与运算 (A && B) 有以下规则：

- 从左开始执行
- 如果A执行后为False，则直接返回False.

- 如果A执行后为True，则继续执行B并返回其值

将递归条件判断放在A，然后具体递归放在B执行，通过A来决定B是否可以运行。此题的A是`n > 1`，B是`n += sumNums(n - 1)`，B后面紧跟着的`> 0`是无意义的，只是用来凑足判断式，触发执行B的内容。

# 题外

初看题目并没有思路，递归算法也不是很熟练，平时都是能不用就不用的，暴力解决一切。这次刚好撞上只能用递归解法，终于来一了次完整的递归展开。

```javascript
/*递归展开*/
function(n = 3) {
    var flag = 3 > 1 && (n = 3 + /*3*/
    function (n = 2) {
        var flag = 2 > 1 && (n = 2 + /*1*/
        function (n = 1) {    
            var flag = 1 > 1 && (n += sumNums(n - 1)) > 0 /*不执行*/
            return n; /*1*/
            };) > 0
        return n; /*3*/
    };) > 0
    return n; /*6*/
};
```

结构递归应该从最里层开始看，一步一步往前推，这里的递归条件`n>1`即`n=1`时递归开始崩溃，崩溃的第一个（最内层）函数返回值就是输入本身（n=1）。递归的思想很巧妙，脑内完整的运行一遍有点困难，所以写递归还是需要套路，需要多加练习。

