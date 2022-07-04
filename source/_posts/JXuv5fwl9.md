---
title: '实现Gridea同步Coding与Github两地仓库'
date: 2020-06-21 10:59:34
tags: [git]
published: true
hideInList: false
feature: 
isTop: false
---
Gridea有一点不好，就是不能同时推送到两个仓库。下面这个方法可以实现Coding与Github两地仓库的同步，解决不能异仓备份博客的问题。
# 步骤
1.登录coding账户
2.进入Coding博客仓库-持续集成-构建计划-新建-简易模板
（[https://你的用户名.coding.net/p/博客仓库名/ci/job/create/simple](https://你的用户名.coding.net/p/博客仓库名/ci/job/create/simple)）
![](https://lafish.fun/post-images/20200621104214.png)
3.随意起名，选择仓库，创建构建计划
4.进入创建的计划-流程配置-文本编辑器
5.删除全部代码，粘贴下面的代码后保存
```
pipeline {
  agent any
  stages {
    stage('检出') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: env.GIT_BUILD_REF]],
          userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]
        ])
      }
    }
    stage('推送部署') {
      steps {
        echo '正在推送文件...'
        sh 'git fetch https://[Github用户名]:[Github令牌]@github.com/[Github用户名]/[Github博客仓库名].git'
        sh 'git push -f https://[Github用户名]:[Github令牌]@github.com/[Github用户名]/[Github博客仓库名].git HEAD:master'
        echo '已完成文件推送.'
      }
    }
  }
}
```
6.设置触发规则：
![](https://lafish.fun/post-images/20200621105155.png)
7.在Gridea中同步一下，看看github上的仓库有没有同步吧！