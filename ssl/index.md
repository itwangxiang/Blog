# SSL 证书申请流程


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

Nginx 配置

```conf
server{
    listen 443 ssl;
    server_name *.wxiang.cc;
    index  index.php index.html index.htm;

    ssl_certificate /etc/nginx/certs/cert;
    ssl_certificate_key /etc/nginx/certs/key;

    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Range $http_range;
        proxy_set_header If-Range $http_if_range;
        proxy_redirect off;
        proxy_pass http://alist:5244;
        # the max size of file to upload
        client_max_body_size 20000m;
    }  
}

server {
    listen       80;
    server_name  *.wxiang.cc;
    return 301 https://$server_name$request_uri;
}
```

