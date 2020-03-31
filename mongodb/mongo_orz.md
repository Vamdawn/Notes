# 踩坑, 埋坑

mongo 使用可视化UI(Robo 3T, mongohub), 或者mongo shell时, 数字字面量类型为"double"!

for example:

```javascript
db.typetest.insertOne({'_id': "0", 'n': 1})
db.typetest.insertOne({'_id': "1", 'n': NumberLong(1)})

db.typetest.find({'n': {$type: "double"}})
// 返回且仅返回第一条数据: {'_id': "0", 'n': 1}
```
