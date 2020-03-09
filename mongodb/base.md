# MongoDB 基本用法

## MongoDB结构

db -> collection -> document -> field

## start

```shell
mongod --dbpath /usr/local/var/mongodb --logpath /usr/local/var/log/mongodb/mongo.log --fork
```

## mongo shell

`mongo shell`是使用javascript进行与mongoDB交互的工具。

在命令行中启动mongo shell

```shell
mongo               # 连接本地默认端口的数据库
mongo --port 28015  # 指定端口
mongo "mongodb://mongodb0.example.com:28015"    # 使用连接字符串连接远程数据库
mongo --host mongodb0.example.com --port 28015  # 使用参数形式连接远程数据库
# 连接时带上用户名和密码
mongo "mongodb://alice@mongodb0.examples.com:28015/?authSource=admin"
mongo --username alice --password --authenticationDatabase admin --host mongodb0.examples.com --port 28015
```

## CRUD Operation

### Insert

```javascript
db.COLLECTION_NAME.insertOne({})            // 插入一条数据
db.COLLECTION_NAME.insertMany([{}, {}])     // 插入多条数据
db.COLLECTION_NAME.insert()                 // 插入一条或多条数据
```

Tips: 如果`_id`字段在插入时被省略，那么MongoDB将自动为`_id`字段生成一个ObjectId

### Query

```javascript
// 基本查询
db.COLLECTION_NAME.find()
db.COLLECTION_NAME.find({"field1": "value1"})
db.COLLECTION_NAME.find({"field1": "value1", "field2": "value2"})
db.COLLECTION_NAME.find({$or: [{"field1": "value1"}, {"field2": "value2"}]})

// 嵌套结构的查询, 使用"."
db.COLLECTION_NAME.find({"filed.nestedField": "value"})

// 限定返回的字段
db.COLLECTION_NAME.find({"filed": "value"}, {"field1": 1, "field2": 1})         // 只返回"field1", "field2", _id字段
db.COLLECTION_NAME.find({"filed": "value"}, {"field1": 1, "field2": 1, _id: 0}) // 不返回_id字段

// 关于null值
db.COLLECTION_NAME.find({"field": null})                // 选出field为null或者field不存在的数据
db.COLLECTION_NAME.find({"field": {$type: 10}})         // 选出field为null的数据, BSON Type null是(type number 10)
db.COLLECTION_NAME.find({"field": {$exists: false}})    // 选出field不存在的数据
```

官方文档对于查询操作符介绍: <https://docs.mongodb.com/manual/reference/operator/query/#query-selectors>

### Update

```javascript
db.COLLECTION_NAME.updateOne(filter, update, options)   // 更新一条
db.COLLECTION_NAME.updateMany(filter, update, options)  // 更新多条
db.COLLECTION_NAME.update(filter, update, options)  // 更新一条或多条
db.COLLECTION_NAME.replaceOne(filter, update, options)  // 取代整个document
// filter筛选出要更新的数据
// update执行更新操作
// options设置额外选项

// $set
db.COLLECTION_NAME.updateOne({"field1": "value1"}, {$set: {"field2": "value2"}})

// upsert, 如果没有document匹配filter，那么创建一条新的document
db.COLLECTION_NAME.updateOne({"field1": "value1"}, {$set: {"field2": "value2"}}, {upsert: true})

// 其他涉及到更新操作的函数
db.COLLECTION_NAME.findOneAndReplace()
db.COLLECTION_NAME.findOneAndUpdate()
db.COLLECTION_NAME.findAndModify()
```

官方文档对于更新操作符的介绍: <https://docs.mongodb.com/manual/reference/operator/update>

### Delete

```javascript
db.COLLECTION_NAME.deleteMany() // 删除多条
db.COLLECTION_NAME.deleteOne()  // 删除一条
db.COLLECTION_NAME.remove()     // 删除一条或多条

// 删除指定collection下所有documents
db.COLLECTION_NAME.deleteMany({})

// 条件匹配的删除
db.COLLECTION_NAME.deleteOne({"field": "value"})

```
