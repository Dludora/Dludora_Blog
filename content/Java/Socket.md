---
title: "Socket"
date: 2022-07-01T16:27:37+08:00
lastmod: 2022-07-01T16:27:37+08:00
description: ""
tags: []
categories: []
author: "codecat"
keywords: []
comment: true
toc: true
autoCollapseToc: true
postMetaInFooter: false
hiddenFromHomePage: false
contentCopyright: true
reward: true
mathjax: true
mathjaxEnableSingleDollar: false
mathjaxEnableAutoNumber: false
---



# 网络多线程

## 一、网络

### 1、相关概念

#### 1.1 ip地址：

1. 概念：用于唯一标识网络中的每台计算机/主机。
2. 查看ip地址：`ipconfig`
3. ip地址的表示形式：点分十进制 `xx.xx.xx.xx`
4. 每一个ip地址的组成=网络地址+主机地址，如：192.168.16.69
5. IPV4：4个字节，IPV6：16个字节

![image-20220701165216171](D:\My Blog\Dludora_Blog\content\Java\image-20220701165216171.png)

#### 1.2 域名

把ip地址映射成域名，`ping 域名`来获取对应ip

## 二、Socket

1. 通信的两端都要有Socket，是两台机器间通信的端点
2. 网络通信其实就是Socket间的通信
3. Socket允许程序把网络连接党曾一个流，数据在两个Socket之间通过IO传输。
4. 一般主动发起通信的应用程序是客户端，等待通信请求的是服务端。

![image-20220701171039264](D:\My Blog\Dludora_Blog\content\Java\image-20220701171039264.png)

![image-20220701171246279](D:\My Blog\Dludora_Blog\content\Java\image-20220701171246279.png)

![image-20220701202741081](D:\My Blog\Dludora_Blog\content\Java\image-20220701202741081.png)
