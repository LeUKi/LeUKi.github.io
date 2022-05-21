---
title: '嵌入式学习小结'
date: 2021-10-28 23:09:33
tags: [嵌入式,linux]
published: true
hideInList: false
feature: 
isTop: false
---
啃了几天的中文网络垃圾，终于算搞明白了一点点。

- 根文件系统与busybox、yaffs的关系

  根文件系统的制作需要用到busybox和yaffs。

  - busybox：

    有人将BusyBox比喻成Linux工具的瑞士军刀，简单的说busybox就是Linux的一个大的工具集，包括了Linux中的大部分命令和工具。

  - yaffs：

    YAFFS文件系统是专门为Nand Flash设计的文件系统，YAFFS目前有yaffs、yaffs2两个版本，yafffs由mkyaffsimage生成，而yaffs2由mkyaffs2image生成，两者的步骤是一样的。

  busybox会在根目录（此处是相对于根文件系统的说法，对于开发机就只是个普通目录，下同）中释放必要的Linux命令文件和工具，yaffs则是将根目录打包成根文件系统镜像。

- uboot与内核与根文件系统的关系

  机器启动首先执行uboot，uboot调起内核，内核挂载根文件系统，再去挂载其他文件系统，挂载完成后才会启动应用程序。

至此才明白了整个流程，内核裁剪、根文件系统与uboot制作的界限逐渐清晰，弄清大局，对于后面的实践就有了信心。