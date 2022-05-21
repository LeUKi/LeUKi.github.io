---
title: '暑期算法 第二题'
date: 2021-08-10 22:19:46
categories: [算法]
published: true
hideInList: false
feature: 
isTop: false
---
# 题目

给你一个字符串 s，找到 s 中最长的回文子串。

> ```
> 输入：s = "babad"
> 输出："bab"
> 解释："aba" 同样是符合题意的答案。
> ```

> ```
> 输入：s = "cbbd"
> 输出："bb"
> ```

> ```
> 输入：s = "a"
> 输出："a"
> ```

> ```
> 输入：s = "ac"
> 输出："a"
> ```

来源：LeetCodeHOT100-5

# 题解

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function (s) {
  if (s.length < 2) {
    return s;
  }
  var res = "";
  for (let i = 0; i < s.length; i++) {
    diff(i, i);//奇数回文扩散
    diff(i, i + 1);//偶数回文扩散
  }

  function diff(m, n) {
    while (m >= 0 && n < s.length && s[m] == s[n]) {
      m--;
      n++;
    }
    if (n - m - 1 > res.length) {//保留最长回文子串
      res = s.slice(m + 1, n);
    }
  }
  return res;
};
```

# 题析

中心扩散法：利用回文子串中心对称的特点，每一个字符都视作为中心，往两边扩散。

偶数子串和奇数子串两种情况都需要考虑。

# 题外

这题暴力也能做，但时间复杂度会到$O(n^3)$。

