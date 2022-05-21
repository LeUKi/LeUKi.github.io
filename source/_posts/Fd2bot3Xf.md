---
title: '一次在jQuery中input绑定keyup等事件的错误记录'
date: 2020-02-24 21:42:03
tags: [JavaScript]
categories: 前端
published: true
hideInList: false
feature: 
isTop: false
---
` $("#s1arch").keyup(alert(123);); `
运行后发现直接运行了alert，找了好久没找到问题。
最后发现是格式错了，正确的写法应该是用一个匿名函数调用代码，而不是直接写代码。
` $("#s1arch").keyup(function(){alert(123);}); `
原因不明，未来找答案。