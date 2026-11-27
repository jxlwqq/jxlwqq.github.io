---
layout: post
title: "《PHP开发APP接口》笔记"
date: 2015-03-25 22:36:00 +0800
categories: php api
---

# PHP开发APP接口

目录

- [PHP开发APP接口](#php开发app接口)
  - [课程地址](#课程地址)
  - [学习要点](#学习要点)
  - [APP接口简介](#app接口简介)
    - [APP接口介绍](#app接口介绍)
      - [概念](#概念)
    - [APP如何进行通信](#app如何进行通信)
    - [通信格式区别](#通信格式区别)
      - [XML定义](#xml定义)
      - [JSON定义](#json定义)
      - [两者的区别](#两者的区别)
    - [APP接口做的哪些事儿](#app接口做的哪些事儿)
      - [获取数据](#获取数据)
      - [提交数据](#提交数据)
      - [APP的常用接口](#app的常用接口)

## 课程地址

[imooc PHP开发APP接口](http://www.imooc.com/learn/163)

## 学习要点

1. APP接口简介
2. 封装通信接口方法
3. 核心技术
4. APP接口实例

> 服务器端 -> 数据库|缓存 -> 调用接口 -> 客户端

## APP接口简介

- APP接口介绍
- APP如何进行通信
- 通信格式区别
- APP接口做的哪些事儿

### APP接口介绍

#### 概念

PHP面向对象的接口(interface)与APP中的接口(API)概念区别：  
interface是一种特殊的抽象类，只定义一系列抽象方法。

```PHP
// 定义一个接口
interface test {
	public function getTest1(); // 抽象方法
	public function getTest2();
}
// 定义一个类实现接口
class demo implements test {
	public function getTest1()
	{
		echo 1;
	}
	public function getTest2()
	{
		echo 2;
	}
}
```

APP接口，也叫通信接口，它必须满足三个条件：

- 接口地址
- 接口文件（处理某些业务逻辑）
- 接口数据

> 客户端：发送APP地址（接口地址）请求  
> 接口地址：返回 JSON|XML格式数据  
> 客户端：解析数据  
> 客户端：填充内容

### APP如何进行通信

APP的通信模式非常类似于浏览器与服务器(B/S)间的通信模式（个人感觉更类似于Ajax的通信模式）。

### 通信格式区别

APP通信格式主要为XML与JSON格式。

#### XML定义

拓展标记语言(Extensible Markup Language, XML)，主要用于标记数据、定义数据类型，是一种允许用户自定义节点的源语言。由于跨平台与跨语言的特性，XML非常适于传输和通信。  
（XHTML是XML的一种应用，也是是HTML的一个子集）。

#### JSON定义

JSON(JavaScript Object Notation)一种轻量级的数据交换格式，具有良好的可读和便于快速编写的特性。可在不同平台之间进行数据交换。JSON采用兼容性很高的、完全独立于语言语言文本格式。

#### 两者的区别

- 可读性
- 生成数据
- 传输速度

```
// JSON数据格式生成方法
// 函数 json_decode()
// XML数据格式生成方法
// 1 字符串拼接
// 2 new DomDocument()
// 3 new XMLWriter()
// 4 new SimpleXml()
```

### APP接口做的哪些事儿

#### 获取数据

从数据库或缓存中获取数据，然后通过接口数据返回给客户端

#### 提交数据

通过接口提交数据给服务器，然后服务器进行入库处理或其他处理操作

#### APP的常用接口

- 版本升级接口
- 获取数据接口
- 提交数据接口

未完待续...博客园的md格式真丑，丢个[evernote的公开链接](http://www.evernote.com/l/AA0Pa-F8Y59I_4l2HQc9ws-Tp7ZgIxEuwYY/)
