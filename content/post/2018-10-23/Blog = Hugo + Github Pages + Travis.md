---
title: "Blog = Hugo + Github Pages + Travis"
date: 2018-10-23T14:04:27+08:00
toc: true
adsense: true
categories:
    - Tech
tags:
    - Hugo
    - Travis
    - Github
---

## 安装 Hugo

```bash
## ubuntu
sudo apt-get install hugo

## windows
choco install hugo -confirm

## macos
brew install hugo
```

## 初始化及安装主题

```bash
## 新建站点
hugo new site blog

## 安装主题
cd blog
git init
git submodule add https://github.com/MunifTanjim/minimo themes/minimo

## Configuration for Minimo
cp themes/minimo/exampleSite/config.toml .
```

p.s. 主题不同，请参考对应主题的安装和配置说明

## 部署到 GitHub pages

### 创建 `<username>.github.io` 仓库

- 在 github 上注册账号并[新建](https://github.com/new)仓库：`<username>.github.io`
- 在 `config.toml` 中的 `baseURL` 设置为 `https://<username>.github.io`

### 提交代码到仓库的 develop 分支

```bash
## 忽略本地生成的 public 文件夹
echo "public" >> .gitignore

## 提交代码
git add -A
git commit -m "initial commit"
git remote add origin https://github.com/<username>/<username>.github.io.git
git push -u origin master:develop
```

### 使用 Travis 自动发布页面到 master 分支

- 生成 [Github Access Token](https://github.com/settings/tokens/new)，勾选 public_repo 的权限
- 到 [Travis](https://travis-ci.org/) 关联 Github，并[激活](https://travis-ci.org/account/repositories) `<username>.github.io` 仓库的自动部署功能
- 在 Travis 的 `<username>.github.io` 仓库配置页中，把生成的 `Github Access Token` 添加到环境变量 `GITHUB_TOKEN`
- 在仓库中添加 `.travis.yml` 配置文件，并 commit 到仓库

```yml
language: go
branches:
  only:
    - develop
install: go get -v github.com/gohugoio/hugo
script: 
  - hugo
deploy:
  provider: pages
  skip_cleanup: true
  github_token: $GITHUB_TOKEN
  local_dir: public
  target_branch: master
  on:
    branch: develop
```

- 在 Travis 手动触发一次仓库 develop 分支的 build 测试效果
- 浏览 `https://<username>.github.io`

## 日常更新操作

1. 更新文章或者配置
2. 提交代码到仓库 

```bash
git add -A
git commint -m "custom comment"
git push -u origin master:develop
```

3. 等待 Travis 发布完成
4. 浏览 `https://<username>.github.io` 并验证更新

## 参考

- https://powersj.io/post/github-hugo/
- https://f4ww4z.me/posts/set-up-hugo/
- https://segmentfault.com/a/1190000012975914
- http://note.qidong.name/2017/07/05/google-analytics-in-hugo/