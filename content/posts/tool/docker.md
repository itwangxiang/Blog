---
title: "Docker 部署记录"
date: "2018-12-05"
tags: [ "docker","部署"]
categories: ["工具"]
---

## [安装](https://docs.docker.com/engine/install/centos/)

```bash
# 脚本安装
## 官方
$curl -sSL https://get.docker.com/ | sh
## 阿里云
$curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun

# centos

$yum update

## 卸载旧版本
$sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
## 使用仓库安装
### 设置一个仓库
$sudo yum install -y yum-utils
#### 官方
$sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
#### 阿里云    
$sudo yum-config-manager \
    --add-repo \
    http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
### 安装最新的引擎
$sudo yum install docker-ce docker-ce-cli containerd.io
### 启动 docker
$sudo systemctl start docker
### 设置随系统重启
$sudo systemctl enable docker
### 设置加速代理（https://mirror.ccs.tencentyun.com）（https://78hmjqgm.mirror.aliyuncs.com）
$sudo mkdir -p /etc/docker
$sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://mirror.ccs.tencentyun.com"]
}
EOF
$sudo systemctl daemon-reload
$sudo systemctl restart docker
### 设置 docker compose https://docs.docker.com/compose/install/
$sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$sudo chmod +x /usr/local/bin/docker-compose
```

## Command

### [Exec](https://docs.docker.com/engine/reference/commandline/exec/)

docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

### [Log](https://docs.docker.com/engine/reference/commandline/logs/)

docker logs [OPTIONS] CONTAINER

- options
  - `--details`
  - `--follow , -f` - 跟踪日志输出
  - `--tail` - 从日志末尾开始显示的行数
  - `--since` - 显示自时间戳记以来的日志（例如2013-01-02T13：23：37）或相对时间（例如42m，持续42分钟）

## 部署示例

### Network

```bash
$sudo docker network create -d bridge --subnet 172.25.0.0/24 mydev;
```

### Mongodb

```bash
# 部署 mongodb://admin:d*w*4**@ip
$sudo docker run -d --restart=always --net mydev --name mongo -h mongo -v mongo-db:/data/db -v mongo-configdb:/data/configdb -p 27017:27017 \
    -e MONGO_INITDB_ROOT_USERNAME=admin \
    -e MONGO_INITDB_ROOT_PASSWORD=****** \
    mongo

# shell 连接, 并登录
$docker exec -it mongo mongo admin
$db.auth('admin','******')

# 设置 db 密码
$use wxiang
$db.createUser({
  user: 'wxiang',  // 用户名
  pwd: '******',  // 密码
  roles:[{
    role: 'dbOwner',  // 角色
    db: 'wxiang'  // 数据库
  }]
})

```

### Mysql

```bash
# 部署 
$sudo docker run -d --restart=always --net mydev --name mysql -h mysql \
    -v mysql-data:/var/lib/mysql \
    -v mysql-config:/etc/mysql/conf.d \
    -p 3306:3306 \
    -e MYSQL_ROOT_PASSWORD=****** \
    mysql

# shell 链接
$docker exec -it mysql mysql -uroot -p 

# 允许 root 远程登录
$grant all privileges on *.* to 'root'@'%' identified by '******' with grant option;

# 设置 db 密码
$CREATE USER 'nacos'@'%' IDENTIFIED BY '******';
$GRANT ALL ON nacos.* TO 'nacos'@'%';
$flush privileges;


# 设置内存 
$docker exec -it mysql bash
$vi /etc/mysql/conf.d/docker.cnf
performance_schema_max_table_instances=400
table_definition_cache=400
table_open_cache=256
performance_schema = off
```

### Redis

```bash
# 部署
$sudo docker run -d --restart=always --net mydev --name redis -h redis -v redis-data:/data -p 6379:6379 \
    redis \
    --requirepass "******"

# shell 链接
$docker exec -it redis redis-cli -a ******
```

### Nacos

```bash
# 部署
$sudo docker run -d --restart=always --net mydev --name nacos -h nacos -p 8848:8848 \
    -e MODE=standalone \
    -e PREFER_HOST_MODE=hostname \
    -e SPRING_DATASOURCE_PLATFORM=mysql \
    -e MYSQL_SERVICE_HOST=mysql \
    -e MYSQL_SERVICE_PORT=3306 \
    -e MYSQL_SERVICE_DB_NAME=nacos \
    -e MYSQL_SERVICE_USER=****** \
    -e MYSQL_SERVICE_PASSWORD=****** \
    -e JVM_XMS=64m \
    -e JVM_XMX=64m \
    -e JVM_XMN=16m \
    -e JVM_MS=8m \
    -e JVM_MMS=8m \
    nacos/nacos-server
```

### jenkins

```bash
$sudo docker run -d --restart=always --net mydev --name jenkins -h jenkins \
  -p 50080:8080 \
  -p 50000:50000 \
  -e JENKINS_JAVA_OPTIONS='-XX:MaxPermSize=512m -Djava.awt.headless=true' \
  -v jenkins-data:/var/jenkins_home \
  -v jenkins-home:/home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkinsci/blueocean
```
