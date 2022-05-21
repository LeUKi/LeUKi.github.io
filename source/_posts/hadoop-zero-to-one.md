---
title: 'hadoop伪分布式从零配置记录'
date: 2022-04-04 17:24:34
tags: [hadoop,大数据]
published: true
hideInList: false
feature: 
isTop: false
---
大数据课给的虚拟机文件只能在win上使用，其他系统引导都进不去，琢磨下怎么从零配置。

虚拟机系统：Ubuntu 20.04.4

# 文件

去镜像站下载比较快

## jdk-8u321-linux-x64.tar.gz

解压到`/usr/local`，命名为java8

## hadoop-3.2.3.tar.gz

解压到`/usr/local`，命名为hadoop

# 环境

系统新建了一个名为hadoop的账户，试了好多错，就按这样来吧

## ~/.bashrc

```bash
export HADOOP_HOME=/usr/local/hadoop
export PATH=$PATH:$HADOOP_HOME/bin
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
export HADOOP_INSTALL=$HADOOP_HOME
export JAVA_HOME=/usr/local/java8
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$CLASSPATH:$JAVA_HOME/lib:$JRE_HOME/lib
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
```

## 安装jre

```bash
sudo apt install default-jre
```

# 配置

## /usr/local/hadoop/etc/hadoop/

### core-site.xml

```xml
<configuration>
   <property>
       <name>hadoop.tmp.dir</name>
       <value>file:/usr/local/hadoop/tmp</value>
       <description>Abase for other temporary directories.</description>
   </property>
   <property>
       <name>fs.defaultFS</name>
       <value>hdfs://localhost:9000</value>
   </property>
    <property>
       <name>hadoop.http.staticuser.user</name>
       <value>hadoop</value>
   </property> 
</configuration>
```

### hdfs-site.xml

```xml
<configuration>
   <property>
       <name>dfs.replication</name>
       <value>1</value>
   </property>
   <property>
       <name>dfs.namenode.name.dir</name>
       <value>file:///usr/local/hadoop/tmp/dfs/name</value>
   </property>
   <property>
       <name>dfs.datanode.data.dir</name>
       <value>file:///usr/local/hadoop/tmp/dfs/data</value>
   </property>
      <property>
       <name>dfs.name.dir</name>
       <value>file:///usr/local/hadoop/tmp/dfs/name</value>
   </property>
   <property>
       <name>dfs.data.dir</name>
       <value>file:///usr/local/hadoop/tmp/dfs/data</value>
   </property>
   <property>
       <name>dfs.http.address</name>
       <value>0.0.0.0:50070</value>
   </property>
</configuration>
```

### hadoop-env.sh

```bash
export JAVA_HOME=/usr/local/java8	
```

### yarn-site.xml

```xml
<configuration>
   <property>
      <name>yarn.nodemanager.aux-services</name>
      <value>mapreduce_shuffle</value> 
   </property>
</configuration>
```

## 初始化

```bash
hadoop namenode -format
```

