---
title: "Flutter"
date: "2019-03-05"
ShowToc: false
ShowBreadCrumbs: false
---

### 基础

#### [安装](https://flutter.dev/docs/get-started/install)

- window
  - `PATH` environment

    ```bash
    # 临时设置环境
    $Env:path += ";D:\_SDK\flutter\bin"

    # 授权系统执行脚本权限
    $set-executionpolicy remotesigned

    # 为当前用户设置环境
    $Add-Content -Path $Profile.CurrentUserAllHosts -Value '$Env:Path += ";D:\_SDK\flutter\bin"'
    ```
