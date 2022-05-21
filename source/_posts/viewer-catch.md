---
title: 'viewer-catch 基于Koa与MongoDB的站点统计平台'
date: 2021-11-08 12:58:11
categories: 前端
published: true
hideInList: false
feature: 
isTop: false
---
> 又是一个练手项目。看了一圈实习招聘条件，大多数前端都要掌握一门后台语言，nodejs 当然是前端开发者的首选。初入前端，我以为我能学成全栈，两年过去这才摸到门槛。~~泪目~~

# 背景

由于我的静态博客没有动态网站的访客统计功能，之前用的是友盟的站长统计，但这个平台 dns 污染严重，体验不是很好。我想要做一个平台，只要简单的引入就实现任意网站、任意页面的统计功能，还要能在页面中插入统计结果，再做一个点赞的功能就更好了。

由此 [`viewer-catch`](https://github.com/LeUKi/viewer-catch)  ~~（原谅我起名废）~~ 应运而生！

# 开始使用！

## 引用

只需要在网站头部添加这一段代码，每一个页面都能分开统计，还支持区分统计 UV 和 PV ，甚至有点赞统计功能！

```html
<script defer src="https://viewer-catch.herokuapp.com/client.js">
```

## 展示

在指定的地方加上类，它能自动替换统计数据，还能控制隐藏显示！

如果需要控制显隐 `.VCC_before` 是必要提前准备的类，推荐是 `visibility: hidden;` 或者 `display: none;` ，当数据类替换完成时它会自动去除。

```html
<style>.VCC_before{visibility: hidden;}</style>
<div class='VCC'>
  <div> 页面UV:<span class='VCC_uv'>正在获取</span> </div>
  <div> 页面PV:<span class='VCC_pv VCC_before'></span> </div>
  <div class='VCC_before'> 页面点赞数:<span class='VCC_like'></span> </div>
</div>
<div class='VCC VCC_before VCC_uv_sum'></div>
<div class='VCC VCC_before VCC_pv_sum' vcc_showin='/'></div>
<div class='VCC VCC_before VCC_like_sum' vcc_hidein='/'></div>
```

## 更简单的使用

对于不用展示数据、没有统计 UV 需求的网站或页面，以下简单引入是更好的方案。

```html
<script sync src="https://viewer-catch.herokuapp.com/simpleCatch?d=xxx.com&p=/path">
```

因标准请求头限制，必须传参使用

- d:Doname 站点域名 必填
- p:Path 页面路径 选填 以 `/` 开头 缺省为 `"/"`

## 更复杂的使用

项目预留了相关接口，可以访问 `/apis` 查看接口文档。

# 关于平台部署

`https://viewer-catch.herokuapp.com/` 部署在 Heroku，每个月只有 550 小时的免费时长，数据库则是用的 `MongoDB Atlas` 的免费套餐 ~~（老白嫖怪了）~~，如果你条件允许可以自己部署平台。你可以参考这篇文章：[利用 MongoDB Atlas 与 Heroku 架设 Free 的后台服务](https://lafish.fun/freedom-service/)

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/LeUKi/viewer-catch)

