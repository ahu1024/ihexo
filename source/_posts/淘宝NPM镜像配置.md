---
title: 淘宝NPM镜像配置
tags:
  - cnpm
  - npm
date: 2018-03-28 09:54:23
updated: 2018-03-28 09:54:23
---

> 淘宝 NPM 镜像是一个完整 npmjs.org 镜像，你可以用此代替官方版本(只读)，同步频率目前为 10分钟 一次以保证尽量与官方服务同步。registry.npm.taobao.org 是从 r.cnpmjs.org 进行全量同步的.
...................................................................................................

# 使用说明

## 直接使用cnpm
```
你可以使用我们定制的 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm:
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
使用方法：
cnpm install express
```

## 间接使用 npm 命令调用cnpm源
```
$ npm config set registry https://registry.npm.taobao.org
查看修改
$ npm config get registry 或者 $ npm info express
修改为默认npm配置:
$ npm config set registry http://registry.cnpmjs.org
```

## 临时使用
```
npm --registry https://registry.npm.taobao.org install express
```