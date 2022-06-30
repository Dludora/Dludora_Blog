---
title: "Java IO流"
date: 2022-06-30T11:42:08+08:00
lastmod: 2022-06-30T11:42:08+08:00
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

# Java IO 流

## 一、文件操作

### 1、创建文件

`new File(String pathname)`	根据路径构建一个File对象

`new File(File parent, String child)`	根据父目录文件+子路径构造

`new File(String parent, String child)`	根据父目录+子路径构建

创建文件对象后,执行  `file.createNewFile`

### 2、获取文件信息

`file.getName()`文件名字

`file.getAbsolutePath()`文件绝对路径

`file.getParent`文件父级目录

`file.length()`文件大小(字节)

`file.exists()` 文件/目录是否存在

`file.isFile()`是否是文件

`file.isDirectory()`是否是目录

### 3、目录操作

`file.delete()`	删除文件/目录

`file.mkdir()`	创建一级目录

`file.mkdirs()`	创建多级目录

### 4、Java IO流原理及其分类

​	I/O是input/output的缩写，按照**操作数据单位**不同分为`字节流`，`字符流`。字节流操作二进制文件时更加适合，字符流操作文本文件更加适合。按照**流的角色**分为`节点流`、`处理流`、`包装流`。

​	**IO流使用完毕后必须关闭!**

| 抽象基类 |    字节流    | 字符流 |
| :------: | :----------: | :----: |
|  输入流  | InputStream  | Reader |
|  输出流  | OutputStream | Writer |

#### 4.1、InputStream

##### 4.1.1 BufferedInputStream	缓冲字节流

##### 4.1.2 FileInputStream	文件字节流

构造方法：

- FIleInputStream(File file)
- FIleInputStream(String filePath)
- FIleInputStream(FileDescription fdObj)

方法

- `int read(byte[] b)`读取一个字节的数据，返回实际读取的字节数。若达到文件末尾，返回-1。如果在其中加入`byte[] b`，则一次获取最多`b.length`字节的数据到字节数组。 可以把`byte`数组转成字符串`new String(b, 0, readLen)`

##### 4.1.3 ObjectInputStream	对象字节流

#### 4.2、OutputStream

##### 4.1.1 FileOutputStream

`FileOutputStream(filePath, append) `如果`append`是`true`而不是`false`时，以追加而不是覆盖的方式写入文件。

- `write(byte[] b, off, len)`会覆盖之前的文件，可以通过`string.getBytes()`把字符串转换为字节数组，输出到对应文件。

### 4.3 Reader

#### 4.3.1 FileReader

与`FileInputStream`类似，读取单位变为字符。

### 4.4 Writer
