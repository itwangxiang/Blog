---
title: "Mongodb"
date: "2019-03-05"
ShowToc: false
ShowBreadCrumbs: false
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
