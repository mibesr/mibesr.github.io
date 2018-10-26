---
title: "Ubuntu 纯命令行版本升级"
date: 2018-10-26T16:25:11+08:00
adsense: true
categories:
    - Tech
tags:
    - Ubuntu
---

1. 安装 update-manager-core

```bash
sudo apt install update-manager-core
```

2. 修改升级通知配置

```bash
sudo vi /etc/update-manager/release-upgrades
```

将 `Prompt` 的值修改为 `normal`

3. 开始升级版本

```bash
sudo do-release-upgrade -d
```

之后，会有一些引导，基本不用管，输入 `y`， 开始升级。

注意：一旦开始升级，中间不能中断，否则，系统大概率会出现问题。



