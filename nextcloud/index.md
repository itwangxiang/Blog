# Nextcloud 部署


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
