---
layout: post
title: "mongodb 学习笔记"
date: 2016-06-23 10:10:00 +0800
categories: mongodb database
---

[evernote\_link](https://www.evernote.com/shard/s13/sh/ce16fe4a-e936-4296-adf4-6fa4f33226ca/17564c04195842f9)

基础教程

http://www.runoob.com/mongodb/mongodb-tutorial.html

官方文档

https://docs.mongodb.com/

SQL与MongoDB的映射关系

如果对关系型数据库比较了解，下面的链接将对你非常有帮助

https://docs.mongodb.com/manual/reference/sql-comparison/

mac安装

brew install mongodb

客户端

robomongo https://robomongo.org/

连接mongodb

mongo

显示所有数据库

show dbs

创建/切换数据库

use test

删除数据库

db.dropDatabase()

插入文档

db.col.inset({"x":10})

db.col.save({"x":11})

删除集合

db.col.drop()

查看所有集合

show collections

定义变量

document = {"y":123};

db.col.insert(document);

更新文档

db.collection.update(

<query>,

<update>,

{

upsert: <boolean>,

multi: <boolean>,

writeConcern: <document>

}

);

- query: update的查询条件
- update: update的对象和一些更新的操作符
- upsert: 可选，如果不存在update的记录，则插入，默认false
- multi: 可选，默认false，只更新找到的第一条记录，true则更新找到的所有记录
- writeConcern: 可选，抛出异常的级别

db.collection.save(

<document>,

{

writeConcern: <document>

}

);

- document:  文档数据
- writeConcern: 可选，抛出异常的级别
- 如果不指定 \_id 字段 save() 方法类似于 insert() 方法。如果指定 \_id 字段，则会更新该 \_id 的数据。

db.col.update({"x":10}, {"x":13}, {upsert:true, multi:true})

db.col.update({"x":10}, {$set: {"x":13}}, true, true)

db.col.save({"x": 10})

db.col.save({“\_id”:”34fdfd343”})

删除文档

db.collection.remove(

<query>,

{

justOne: <boolean>,

writeConcern: <document>

}

)

db.col.remove({“x”: 13});

查询文档

db.col.find()

db.col.findOne()

db.col.find().pretty()

db.col.find({"x":12})

db.col.find({"x":{$eq:12}})

db.col.find({"x":{$lt:12}})

db.col.find({"x":{$lte:12}})

db.col.find({"x":{$gt:12}})

db.col.find({"x":{$gte:12}})

db.col.find({"x":{$ne:12}})

db.col.find({"x":12,"x”:{$ne:13}})

db.col.find({$or:[{"x":12},{"x":13}]})

$type操作符

$type操作符是基于BSON类型来检索集合中匹配的数据类型，并返回结果

| 类型 | 数字 | 备注 |
| --- | --- | --- |
| Double | 1 |  |
| String | 2 |  |
| Object | 3 |  |
| Array | 4 |  |
| Binary data | 5 |  |
| Undefined | 6 | 已废弃。 |
| Object id | 7 |  |
| Boolean | 8 |  |
| Date | 9 |  |
| Null | 10 |  |
| Regular Expression | 11 |  |
| JavaScript | 13 |  |
| Symbol | 14 |  |
| JavaScript (with scope) | 15 |  |
| 32-bit integer | 16 |  |
| Timestamp | 17 |  |
| 64-bit integer | 18 |  |
| Min key | 255 | Query with -1. |
| Max key | 127 |  |

db.col.find({"x":{$type:2}})

limit与skip

db.col.find({"x":12}).limit(2)

db.col.find({"x":12}).skip(2)

sort排序

db.col.find().sort({"x":1})

db.col.find().sort({"x":-1})

index索引

# 创建索引

db.col.ensureIndex({"x”:1})

db.col.ensureIndex({"x":-1})

db.col.ensureIndex({"x":1, "y":-1})

| Parameter | Type | Description |
| --- | --- | --- |
| background | Boolean | 建索引过程会阻塞其它数据库操作，background可指定以后台方式创建索引，即增加 "background" 可选参数。 "background" 默认值为**false**。 |
| unique | Boolean | 建立的索引是否唯一。指定为true创建唯一索引。默认值为**false**. |
| name | string | 索引的名称。如果未指定，MongoDB的通过连接索引的字段名和排序顺序生成一个索引名称。 |
| dropDups | Boolean | 在建立唯一索引时是否删除重复记录,指定 true 创建唯一索引。默认值为 **false**. |
| sparse | Boolean | 对文档中不存在的字段数据不启用索引；这个参数需要特别注意，如果设置为true的话，在索引字段中不会查询出不包含对应字段的文档.。默认值为 **false**. |
| expireAfterSeconds | integer | 指定一个以秒为单位的数值，完成 TTL设定，设定集合的生存时间。 |
| v | index version | 索引的版本号。默认的索引版本取决于mongod创建索引时运行的版本。 |
| weights | document | 索引权重值，数值在 1 到 99,999 之间，表示该索引相对于其他索引字段的得分权重。 |
| default\_language | string | 对于文本索引，该参数决定了停用词及词干和词器的规则的列表。 默认为英语 |
| language\_override | string | 对于文本索引，该参数指定了包含在文档中的字段名，语言覆盖默认的language，默认值为 language. |

db.col.ensureIndex({"x":1}, {background: true})

聚合

db.col.drop()

db.col.insert({

title: 'MongoDB Overview',

description: 'MongoDB is no sql database',  
  by\_user: 'w3cschool.cc',  
  url: 'http://www.w3cschool.cc',  
  tags: ['mongodb', 'database', 'NoSQL'],

likes: 100

})

db.col.insert({

title: 'NoSQL Overview',  
  description: 'No sql database is very fast',  
  by\_user: 'w3cschool.cc',  
  url: 'http://www.w3cschool.cc',  
  tags: ['mongodb', 'database', 'NoSQL'],

likes: 10

})

db.col.insert({

title: 'Neo4j Overview',  
  description: 'Neo4j is no sql database',  
  by\_user: 'Neo4j',  
  url: 'http://www.neo4j.com',  
  tags: ['neo4j', 'database', 'NoSQL'],

likes: 750

})

db.col.aggregate([{$group:{\_id:"$by\_user", num\_tutorial:{$sum:1}}}])

| 表达式 | 描述 | 实例 |
| --- | --- | --- |
| $sum | 计算总和。 | db.mycol.aggregate([{$group : {\_id : "$by\_user", num\_tutorial : {$sum : "$likes"}}}]) |
| $avg | 计算平均值 | db.mycol.aggregate([{$group : {\_id : "$by\_user", num\_tutorial : {$avg : "$likes"}}}]) |
| $min | 获取集合中所有文档对应值得最小值。 | db.mycol.aggregate([{$group : {\_id : "$by\_user", num\_tutorial : {$min : "$likes"}}}]) |
| $max | 获取集合中所有文档对应值得最大值。 | db.mycol.aggregate([{$group : {\_id : "$by\_user", num\_tutorial : {$max : "$likes"}}}]) |
| $push | 在结果文档中插入值到一个数组中。 | db.mycol.aggregate([{$group : {\_id : "$by\_user", url : {$push: "$url"}}}]) |
| $addToSet | 在结果文档中插入值到一个数组中，但不创建副本。 | db.mycol.aggregate([{$group : {\_id : "$by\_user", url : {$addToSet : "$url"}}}]) |
| $first | 根据资源文档的排序获取第一个文档数据。 | db.mycol.aggregate([{$group : {\_id : "$by\_user", first\_url : {$first : "$url"}}}]) |
| $last | 根据资源文档的排序获取最后一个文档数据 | db.mycol.aggregate([{$group : {\_id : "$by\_user", last\_url : {$last : "$url"}}}]) |
