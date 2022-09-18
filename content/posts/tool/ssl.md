---
title: "SSL 证书申请流程"
date: "2022-09-18"
tags: [ "ssl","部署"]
categories: ["工具"]
---

## SSL 证书申请流程

简单申请，记录下

### 使用 acme - dns 方式申请

设置 CA

```bash
docker run --rm  -it  \
  -v $PWD/acme:/acme.sh  \
  neilpang/acme.sh  --set-default-ca --server letsencrypt
```

注册

```bash
docker run --rm  -it  \
  -v $PWD/acme:/acme.sh  \
  neilpang/acme.sh  --register-account -m ***@gmail.com
```

申请证书

```bash
docker run --rm  -it  \
  -v $PWD/acme:/acme.sh  \
  neilpang/acme.sh  --issue -d *.wxiang.cc  --dns --yes-I-know-dns-manual-mode-enough-go-ahead-please
```

更新证书

```bash
docker run --rm  -it  \
  -v $PWD/acme:/acme.sh  \
  neilpang/acme.sh  --renew -d *.wxiang.cc  --dns --yes-I-know-dns-manual-mode-enough-go-ahead-please
```

导出证书(nginx)

```bash
docker run --rm  -it  \
  -v $PWD/acme:/acme.sh  \
  neilpang/acme.sh --install-cert -d uind.wxiang.cc \
  --cert-file /acme.sh/certs/cert \
  --key-file /acme.sh/certs/key \
  --fullchain-file /acme.sh/certs/fullchain

```
