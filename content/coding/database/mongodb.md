---
title: "Mongodb 常用命令"
date: "2020-03-14"
tags: [ "mongodb"]
categories:
  - "数据库" 
---
# Mongodb

## 常用命令

### aggregate

求和

```shell
db.app_log.aggregate([
   { $match: { userId: "kim", type: "use" } },
   { $group: { _id: {}, total: { $sum: "$useTime" } } },
   { $project: {_id: 0, total: 1}}
])
```
