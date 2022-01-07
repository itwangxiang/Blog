---
title: "Golang 编译命令"
date: "2018-04-18"
ShowToc: false
ShowBreadCrumbs: false
tags: [ "go","命令"]
categories:
  - "开发" 
---

### 交叉编译

Mac 下编译

```bash
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build main.go
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go
```

Linux 下编译

```bash
# mac
CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build main.go
# windows
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go
```

Windows 下编译

```bash
# mac
SET CGO_ENABLED=0
SET GOOS=darwin
SET GOARCH=amd64
go build main.go

#linux
SET CGO_ENABLED=0
SET GOOS=linux
SET GOARCH=amd64
go build main.go
```
