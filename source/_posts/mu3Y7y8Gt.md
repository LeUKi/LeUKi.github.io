---
title: 'DW1820A黑苹果网卡简单折腾记录'
date: 2020-03-01 22:00:40
categories: [黑苹果]
published: true
hideInList: false
feature: 
isTop: false
---
> 更新了，前面的方法不完美，请看后面！

哪个男孩不想拥有一张完美的黑苹果网卡？（误）
无奈钱包瘪瘪，DW1830和DW1560对于目前学生的我实在太过昂贵。直到某天，在闲鱼上让我刷到了这“物美价廉”玩意。竟然只要1/4的价钱，就能体验到msata免驱的WiFi加蓝牙。
到货装上后WiFi能免驱显示，但蓝牙却没反应。远景上也有人发过类似的帖子，顺着帖子找到了小兵大佬在19年8月份发的博客：[DW1820A...插入的正确姿势](https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html)
来回折腾了几次，稳定版2.2.10文件和10.14测试版2.5.1文件在macOS1.14.6中只支持airdrop和handoff，并不能连接耳机和触控板等外设。只有10.15测试版2.5.1能近完美驱动这张网卡。
![](https://lafish.fun/post-images/1583073715577.png)
![](https://lafish.fun/post-images/1583073720233.png)
![](https://lafish.fun/post-images/1583073724880.png)
这张廉价网卡也是有缺点的，WiFi蓝牙共用2.4G会导致蓝牙不稳定，也不能连接5GWiFi的信号，虽然还能折腾下，但能用就行，觉得再弄下去没完没了。
记录几个还没有试过的方法：
- 从Windows热重启到macOS
- 关机拔掉电源，等待5分钟再加电开机（但我这笔记本把电源不靠谱）
---
> 20200328更新！找到了一个更好的方法，完美实现蓝牙功能，而且还解决了不能连接5Gwifi的问题，修复了开机几率掉蓝牙的问题。

参考的是远景网友分享出来的方法：[关于DW1820A蓝牙连接问题解决方法，其它应该也可以。](http://bbs.pcbeta.com/viewthread-1802647-1-1.html)
很巧的是我买到的网卡和他的一样，在IOKitPersonalities添加子节后，把开头安装的2.5.1文件删除，重新下载稳定版本[v2.2.10](http://7.daliansky.net/DW1820A/BT_for_DW1820A_Ver.2.zip)解压到` /EFI/CLOVER/kexts/Other `目录下，重启搞定！
需要注意的是远景教程里给出代码的第一行是多余的，重复添加可能会无法开机。
这里贴上我的Info.plist：
``` 
<key>Broadcom</key>
    <dict>
        <key>CFBundleIdentifier</key>
            <string>com.apple.iokit.BroadcomBluetoothHostControllerUSBTransport</string>
        <key>IOClass</key>
            <string>BroadcomBluetoothHostControllerUSBTransport</string>
        <key>IOProviderClass</key>
            <string>IOUSBHostDevice</string>
        <key>idProduct</key>
            <integer>25618</integer>
        <key>idVendor</key>
            <integer>2652</integer>
    </dict>
``` 
至此，我离完美的黑苹果更进一步啦！如果你看到这，也祝你成功。

