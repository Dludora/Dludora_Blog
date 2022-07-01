---
title: "多线程"
date: 2022-06-30T20:38:02+08:00
lastmod: 2022-06-30T20:38:02+08:00
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



# 多线程

- 程序：我们写的代码
- 进程：运行中的程序，是程序的一个执行过程

## 一、继承Thread类（重写 run 方法）

​	当一个类继承了`Thread`类，该类就可以当作线程使用。我们会重写`run`方法，写上自己的业务代码。`run Thread`类实现了`Runnable`接口中的`run`方法。通过`start`方法启动线程。

​	使用`JConsole`监控线程执行情况，并画出程序示意图。(命令行输入`jconsole`)

```java
public class Thread01 {
    public static void main(String[] args) throws InterruptedException {

        // 创建Cat对象，可以当作线程使用
        Cat cat = new Cat();
        cat.start();    // 启动线程->最终会执行cat的run方法
        // 当main线程启动一个子线程Thread-0，主线程不会阻塞，会继续执行

        System.out.println("主线程继续执行" + Thread.currentThread().getName());
        for (int i = 0; i < 10; i++) {
            System.out.println("主线程 i = "+ i);
            // 让主线程休眠
            Thread.sleep(1000);
        }
    }
}

class Cat extends Thread {
    int times = 0;
    @Override
    public void run() {
        while (true) {
            // 该线程每隔一秒，在控制台输出"喵喵，我是小猫咪"
            System.out.println("喵喵，我是小猫咪" + (++times) + " 线程名=" + Thread.currentThread().getName());
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            if (times == 8) {
                break;
            }
        }
    }
}
```

## 二、实现Runnable接口

**说明**

- Java是单继承的，在某些情况下一个类可能已经继承了某个父类，这时无法再继承Thread类方法来创建进程。
- 可以通过实现`Runnable`接口来创建线程

```java
public class Thread02 {
    public static void main(String[] args) {
        Dog dog = new Dog();
        // 这里不能直接 调用start()方法
        Thread thread = new Thread(dog);
        thread.start();
    }
}

class Dog implements Runnable {
    int count = 0;

    @Override
    public void run() {
        while (true) {
            System.out.println("小狗汪汪叫..hi" + (++count) + Thread.currentThread().getName());

            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

## 三、线程方法

`setName`、`getName`、`start`、`run`、`setPriority`、`getPriority`、`sleep`、`interrupt`

### 1、线程礼让（yield）

​	让出CPU，让其他线程执行，但礼让的时间不确定，也不一定礼让成功（资源充足时）。

### 2、线程插队（join）

插队的线程一旦插队成功，则肯定先执行完插入的线程的所有任务。

```java
package threaduse;

public class Thread03 {
    public static void main(String[] args) {
        T1 t1 = new T1();
        t1.start();

        for (int i = 1; i <= 20; i++) {
            try {
                Thread.sleep(1000);
                System.out.println("主线程 吃了" + i + " 个包子");
                if (i == 5) {
                    System.out.println("主线程让 子线程 先全部吃完");
                    t1.join();      // 相当于让t2线程先执行完毕。
                    System.out.println("子线程 全部吃完，主线程接着吃");
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

class T1 extends Thread {
    @Override
    public void run() {

        for (int i = 1; i <= 20; i++) {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("子线程 吃了" + i + " 个包子");
        }
    }
}
```

### 3、用户线程和守护线程

1. 用户线程：也叫哦工作线程，当线程的任务执行完或通知方式结束
2. 守护线程：一般是为工作线程服务，当所有用户线程结束，守护线程自动结束
3. 常见守护线程：垃圾回收机制。

**设置某一线程为守护线程**，在线程开始之前执行语句：`Thread.setDaemon(true)`

## 四、锁

解决**超卖问题**

### 1、线程同步机制

1. 在多线程编程，一些敏感数据不允许被多个线程同时访问，使用同步访问计数，保证数据在任何同一时刻，最多有一个线程访问，保证数据的完整性。
2. 当有一个线程在对内存进行操作时，其他线程都不可以对这个内存地址进行操作，知道该线程完成操作。

### 2、同步方法

#### 2.1 同步

```java
synchronized(对象) {	// 得到对象的锁
	// 需要被同步的代码
}
```

```java
public synchronized void m(String name) {
	// 需要被同步的代码
}
```

#### 2.2 互斥锁

