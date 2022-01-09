# Windows 常用命令


## 开发环境

使用 Scoop 搭建开发环境

```powershell
#########################################################
##################     Scoop Install    #################
#########################################################

##### Set ExecutionPolicy
Set-ExecutionPolicy RemoteSigned -scope CurrentUser

##### Custom Path
$env:SCOOP='D:\wxiang\Scoop'
[environment]::setEnvironmentVariable('SCOOP',$env:SCOOP,'User')
iwr -useb get.scoop.sh | iex

##### Set Proxy
scoop config proxy 127.0.0.1:1080

##### GIT
scoop install git
git config --global user.name "itwangxiang"
git config --global user.email "itwangxiang@foxmail.com"

##### Add Bucket
scoop bucket add extras
scoop bucket add nirsoft
scoop bucket add java
scoop bucket add jetbrains

#########################################################
##################     App Install    ###################
#########################################################

##### CLI tools
scoop install sudo
scoop install curl
scoop install wget
scoop install aria2
scoop install zip

## Config
#scoop install concfg
#concfg export console-backup.json
#concfg import solarized-dark

## SSH
#scoop install win32-openssh
##ssh-keygen
##cat ~/.ssh/id_rsa.pub | ssh root@wxiang.cc 'mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys'


##### GUI Software

##
scoop install vscode
scoop install IntelliJ-IDEA-Ultimate

## Tool
scoop install vim
scoop install windows-terminal
scoop install beyondcompare
scoop install sublime-text

scoop install postman
#scoop install xmind8 # 思维导图
#scoop install jmeter # 压力测试


##### SDK
scoop install openjdk8-redhat
```

