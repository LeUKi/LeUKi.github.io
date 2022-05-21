---
title: '利用 MongoDB Atlas 与 Heroku 架设 Free 的后台服务'
date: 2021-10-23 22:24:11
tags: [nodejs]
categories: 前端
published: true
hideInList: false
feature: 
isTop: false
---
> Free：自由、开源、免费！白嫖！

# 前言

MongoDB Atlas 是 MongoDB 官方提供的线上数据库服务，免费的 M0 Sandbox 档提供 512MB 的容量，有谷歌台湾和微软香港节点可选。

Heroku 是一个云计算平台，注册用户每个月有550小时的免费计算资源，如果验证了新银行卡还能再加450小时和域名绑定。30分钟不活动就会进入睡眠状态，有新需求的时候就会自动重启。有很多语言环境可选，这里我们用到的是 nodejs。

# 开始动手

我写了一个练手的后台项目，详情可以见后面发的文章，这次的目的就是把服务架设起来。

## 代码调整

如果是 nodejs 项目，Heroku 启动程序会调用 npm start， 所以确保 package.js 中写好名为 start 的脚本。

```json
//package.js
{
  ...,
  "scripts": {
  	...
    "start": "node app.js" //程序入口
  },
	...
}
```

## 链接Github仓库

Heroku 项目的 Deploy 选项中绑定 Github 仓库，如此当你提交代码后，Heroku 会自动拉取新代码并启用新的代码程序。

![Deploy Github](https://lafish.fun/post-images/1634999417834.png)

## 配置环境变量

当存在私有代码例如数据库地址与秘钥、第三方 token 时，就可以用环境变量来解决。

在项目使用私有代码地方填充 ```process.env.XXX```，并在 Heroku 项目的 Setting - Config Vars 选项中填入对应的值，在运行程序前这些环境变量就会被替换。

![Config Vars](https://lafish.fun/post-images/1634999401675.png)

## 运行！

可以看到接口服务跑起来了，也能成功对接数据库。当半小时没有访问流量，服务关闭，当我们再次访问接口时，Heroku 重启了程序，服务启动需要约3秒的时间，还是很理想的。~~（毕竟白嫖的嘛）~~

![Heroku Project Log](https://lafish.fun/post-images/1634999351965.png)

# 最后

对于类似这种性能要求不高、并发量不大的个人流量统计服务，架设到这种地方确实不失为~~省钱小妙招~~有趣的解决方案。希望国内的厂商能为个人提供类似的开源免费计算服务，虽然需要多折腾点，但当你的代码没有金钱的束缚，在广阔的网络中自由奔跑，那想想还真是不错呢。

