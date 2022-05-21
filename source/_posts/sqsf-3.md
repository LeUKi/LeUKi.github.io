---
title: '暑期算法 第三题'
date: 2021-08-11 23:59:59
categories: [算法]
published: true
hideInList: false
feature: 
isTop: false
---
# 题目

给定一个只包括` '('，')'，'{'，'}'，'['，']' `的字符串 s ，判断字符串是否有效。

有效字符串需满足：

- 左括号必须用相同类型的右括号闭合。
- 左括号必须以正确的顺序闭合。

> ```
> 输入：s = "()"
> 输出：true
> ```

> ```
> 输入：s = "()[]{}"
> 输出：true
> ```

> ```
> 输入：s = "(]"
> 输出：false

> ```
> 输入：s = "([)]"
> 输出：false
> ```

> ```
> 输入：s = "{[]}"
> 输出：true
> ```

来源：LeetCodeHOT100-20

# 题解

```javascript
var isValid = function (s) {
  const stack = [];
  for (let i = 0; i < s.length; i++) {
    let c = s[i];
    switch (c) { //如果是左括号，对应有括号入栈
      case '(':
        stack.push(')');
        break;
      case '[':
        stack.push(']');
        break;
      case '{':
        stack.push('}');
        break;
      default: //如果是右括号，栈顶取出并比对
        if (c !== stack.pop()) {
          return false;
        }
    }
  }
  return stack.length === 0; //确保没有多余的括号
};
```

# 题析

使用栈实现，遍历时直接压入对应的字符，等右括号来了再比对，符合的就出栈，最后检查剩余字符，确保没有左右括号多余的情况。

# 题外

使用哈希表会有更简洁的写法。

```javascript
var isValid = function(s) {
    const stack = [], 
        map = {
            "(":")",
            "{":"}",
            "[":"]"
        };
    for(const x of s) { //遍历s
        if(x in map) { 
            stack.push(x);
            continue;
        };
        if(map[stack.pop()] !== x) return false; //此处使用了哈希表
    }
    return !stack.length;
};
```

一道水题，但看完后大为惊讶，原来能这么简单，前次比赛有遇到，想着简单但就是写不出来，看来还是水平不够。