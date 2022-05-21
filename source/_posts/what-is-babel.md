---
title: '初识 Babel'
date: 2021-10-07 22:08:18
tags: [Babel]
categories: 前端
published: true
hideInList: false
feature: 
isTop: false
---
# 什么是 Babel

Babel 是一个 JavaScript 编译器，是当下前端工程化开发必不可缺的一环，它最主要的作用是语法降级和源码转换。有了 Babel ，写的 ES6 语法能跑在 IE，React 优雅的 JSX 语法开发才得以实现。

使用 Vue / React 等框架的脚手架生成项目，无一例外集成了 Babel，你可以在项目目录中轻松找到 Babel 的存在。

![react项目中的Babal配置](https://lafish.fun/post-images/1633615964818.png)
![vue项目中的Babal配置](https://lafish.fun/post-images/1633615924098.png)

通常情况下，脚手架作者已经将 Babel 配置妥当，无需二次调试。



# 让我们试试

## 准备测试环境

```json
//package.json 新建
{
  "devDependencies": {
    "@babel/cli": "^7.15.7",
    "@babel/core": "^7.15.5",
    "@babel/preset-env": "^7.15.6"
  },
  "dependencies": {
    "@babel/polyfill": "^7.12.1"
  }
}
```

使用 `npm i` 或 `yarn insatll` 安装好包依赖。

## 配置Babel

常见的方法是将配置写入工程根目录的 `babel.config.json`（如上图Vue-Cli生成的文件）或 `.babelrc.json` ，再或者直接写进 `package.json`。

```json
//package.json 追加
{
  ...,
  "babel": {
    "presets": [
      [
        "@babel/env",
        {
          "targets": {
            "chrome": "60"
          },
          "useBuiltIns": "usage",
          "corejs": "3.6.5"
        }
      ]
    ]
  }
}
```

- 在这里我们指定 `"presets"` 的第一项为 `@babel/env`，这是上文安装好的 `@babel/preset-env` 的缩写，是官方提供的预设，提供了 ES2015+ 的语法转换。在 Vue-Cli 中，该项为 `@vue/cli-plugin-babel/preset`，由 Vue-Cli 作者开发。

- `"presets"` 的第二项是该预设的参数，`@babel/env` 规定当无传参时，默认转换至 ES5 语法兼容。
  - 此处 `"targets"` 指定了代码最低兼容的环境是 chrome v60
  - `"useBuiltIns": "usage"` 导入了作为依赖的`@babel/polyfill`，其为 ES6+ 的语法降级提供了替换代码
  - `corejs` 指定了babel核心 `@babel/core` 的具体版本

## 启动！

配置好 Babel 后，让我们研究下怎么启动它。

作为开发依赖的 `@babel/cli` 提供了内部指令，使用 `node_modules/.bin/babel` 我们就可以启动 Babel 了，当然 node 为了内部模块的方便使用，增加了 npx 命令，你还可以这样调用它。

```bash
# npx babel => node_modules/.bin/babel
npx babel src --out-dir dist
```

- 第一项参数表示输入的源代码目标文件夹或文件，在这里我们指定编译 `src/` 下所有的文件

- 第二项 `--out-dir` 可选参数表示编译后输出的文件目录，在这里我们指定编译输出至 `dist/` 文件夹中

现在让我们在 `src/` 中创建一个 `app.js`，输入一些 ES6+ 代码，保存文件，输入脚本指令，Babel 就会自动编译并保存在 `dist/` 了。

![第一次手动编译](https://lafish.fun/post-images/1633616072839.png)

显示成功了，`dist/app.js` 也填充了编译后的代码，但我们发现并没有什么变化。这是因为我们在 `package.json` 中配置的转换目标是 chrome v60，它已经支持了 class 和箭头函数语法。想看点不一样的，让我们把配置拉低”亿“点。

```json
//package.json 新增
{
  ...,
  "babel": {
    "presets": [
      [
        "@babel/env",
        {
          "targets": {
            "chrome": "60",
            "ie": "11"
          },
          "useBuiltIns": "usage",
          "corejs": "3.6.5"
        }
      ]
    ]
  }
}
```

这次我们增加了臭名昭著的 IE 浏览器，版本是 2013 年最新推出的 IE11，它仍将持续服役至 2022 年。

# 加点料

暂停一下，带你认识一个好用的工具——nodemon。

nodemon 的作用很简单，监听文件变化，并执行一些命令。使用 `npm i nodemon -D`或`yarn add nodemon -D` 安装，这里 `-D` 指将它作为开发依赖安装。

```bash
nodemon --watch src --exec npx babel src --out-dir dist
```

- `--watch` 指监听的文件或文件夹，这里我们要监听 `src/` 中的文件
- `--exec` 指文件变动后运行的指令，这里就填入上文的指令

将 nodemon 跑起来，现在当我们在 `src/` 中保存文件时，nodemon 就会触发指令，Babel 也会自动转换代码到 `dist/` 中了。

![保存自动编译](https://lafish.fun/post-images/1633616089808.gif)

有内味了，就像是 Vue 和 React 一样。看编译后的代码可以发现，Babel 将箭头函数直接转换成了普通函数，class 语法则是引入了 Babel 的 `_createClass` 辅助函数，以ES5语法实现了 ES6 的功能。

# 结束

这次测试，没有深入剖析 Babel 的原理，只是简单上手实现了基础的保存自动转换功能，但我们仍能从中窥见前端底层技术的魅力，新的标准未有确定，但我们依然能在现有的框架下实现新东西，正是这样的超前应用推动了前端不断发展、愈发繁华。

实际项目中，我们很少会去调试 Babel，因为各种脚手架已经为我们铺垫好了道路。这篇文章希望能予你些启发，或许不会再有更多的调试，但它们确实为前端工程化发展打下了坚实的基础。