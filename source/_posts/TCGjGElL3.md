---
title: '关于Minecraft(Java1.12.2)服务器中“删除”作浮空字盔甲架的新方法'
date: 2020-02-06 11:24:04
tags: [Minecraft]
published: true
hideInList: false
feature: 
isTop: false
---
> 单机作弊模式下也可参考！急的跳过前言看后面

# 前言
利用summon指令生成了一个浮空字，原理是生成一个隐形的盔甲架并把其名字做常显示。

```java
 /summon minecraft:armor_stand ~ ~2 ~ {Marker:1,NoGravity:1,Invisible:1,CustomNameVisible:1,CustomName:"这是串浮空的字"}
 ```

但当我们想删除它时，输入 **/kill @e[type=armor_stand,c=10]** 指令可能会出现 **Error: Player not found.** 的报错论坛也有说用 **/killall** 指令的，但实测无用。

网上也没用人给出删除的办法，似乎这是个bug。有人给出下下策，删除区块甚至删除存档。我想这条生成指令正常玩家大概率不会用到。使用的大多数是地图制作者和服务器op，前者可以回档重来，后者一般用相关插件管理，用的人寥寥无几。似乎没有删除的需求，但真遇上了也是件恶心的事，所以下面给出方法。

# 新方法
利用**entitydata**指令更改实体的属性参数，这是1.8版本中加入的指令，一般用作给全地图怪物加装备。

```java
/entitydata @e[type=Armor_Stand,r=10] {CustomNameVisible:0}
```

将CustomNameVisible(名字可见度)设置为不可见(0)，实际上这个实体并没有被删除，而是完全隐藏了。