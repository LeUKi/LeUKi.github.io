---
title: '关于C语言printf函数的易错点'
date: 2019-12-01 08:48:51
tags: [C语言]
published: true
hideInList: false
feature: 
---
截取了这样一段代码：
```c
int a=1;
printf("%d,%d",++a,a);
```
会输出什么呢？
答案不是`2,2`，而是`2,1`。
原来printf函数是同赋值变量具有右结合性的，而这在教材中鲜少提到。