---
layout: post
title: "MySQL性能优化经验"
date: 2016-06-16 10:11:00 +0800
categories: mysql performance
---

##

### 核心

- 不做运算 `md5()` `Order By Rand()`
- 控制单表数据量
- 保持表字段苗条
- 平衡范式与冗余
- 拒绝3B `Big SQL` `Big Transaction` `Big Batch`

### 字段

- 用好数值字段类型
- 将字符转为数字 `IP`
- 优先使用枚举 ``` ENUM``SET ```
- 避免使用`NULL`字段
- 少用并拆分`TEXT`/`BLOB`
- 不存图片

### 索引

- 谨慎合理添加索引 `20%`
- 字符字段必须建前缀索引
- 不在索引列做运算
- 自增列或全局ID做InnoDB`主键`
- 尽量不用`外键`

### SQL

- SQL语句尽可能简单
- 保持事务（连接）短小
- 避免使用`SP`/`TRIG`/`FUNC`
- 避免使用 `SELECT *`
- 改写`OR`语句 `IN` `UNION`
- 避免`负向`查询和`%前缀模糊`查询
- 减少`COUNT(*)`
- `LIMIT`高效分页
- 用`UNION ALL`而非`UNION`
- 分解联接保证高并发
- `GROUP BY`去除排序
- 同数据类型的列值比较
- `Load data`导数据
- 打散大批量更新 `SLEEP`
- Know Every SQL

### 约定

- 隔离线上线下
- 禁止未经DBA确认的子查询
- 永远不在程序端显式加锁
- 统一字符集为UTF8
- 统一命名规范
