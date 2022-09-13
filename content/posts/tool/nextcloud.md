---
title: "Nextcloud 部署"
date: "2022-09-09"
tags: [ "cloud","部署"]
categories: ["工具"]
---

## Nextcloud 部署

### 安装

```bash
docker run -d \
--restart=always \
--name ncloud \
-v ncloud:/var/www/html \
-v /mnt/nextcloud/data:/var/www/html/data \
-p 5555:80 \
--link mysql \
nextcloud
```