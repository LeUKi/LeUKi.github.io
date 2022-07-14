---
title: 写一个简单的工具库
tags:
  - typescript
  - npm
categories:
  - 前端
comments: true
date: 2022-07-14 16:51:55
---
这几天在把之前写的一些工具类代码做个库开源出来，第一版自用的实在寒碜，要捯饬捯饬用ts重写一遍。

代码流程是用tsc转换代码，webpack打包。已经重写了一部分，但测试居然跑不通！一查果然是commonjs和esmodule的锅。

找了很多办法，发现webpack不能用来转换，这应该是babel的功能。其实webpack也是不需要的，就应该源码提交，方便其他开发者修改，需要压缩代码时他们肯定会用webpack的。

这个工具的主要功能就是按规则批量生成编码，编码这个词在英语不好翻译，怎么写都觉得会有歧义。其实就是生成很多条字符串，这些字符串有规律，比如`["xxx1", "xxx2", "xxx3", ...]`、`["1.0.0", "1.2.0", "1.4.0", ...]`、`["peop-A", "peop-B", "peop-C", ...]`。

设计了一套短编码，对应上面三个生成规则：`"1:1000:1:x"`、`"1. 0:9:2"`、`"peop- A:Z"`，每个子规则间用空格分割。

codes-generator-js：[github](https://github.com/LeUKi/codes-generator-js) [NPM](https://registry.npmjs.org/codes-generator-js)

写的很乱，以后再优化吧。