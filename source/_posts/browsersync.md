---
title: Hexo 通过 browsersync 让 浏览器 自动刷新
date: 2025-05-08 01:00:24
tags:
---

> 转自: https://blog.singee.me/2018/05/16/hexo/hexo-auto-refresh/

效果：修改 Markdown 文件并保存后浏览器可以自动刷新

## Step 1. 安装 Browsersync
在任意目录下执行
```
npm install -g browser-sync
```
安装完成后利用 `browser-sync --version` 来检测是否安装成功

## Step 2. 安装 Hexo 插件

在 Hexo 目录下执行
```
npm install hexo-browsersync --save
```

## Step 3. 启动测试
使用 `hexo s` 启动服务即可
