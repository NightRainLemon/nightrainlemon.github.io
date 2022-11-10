---
title: npm 更改镜像源
categories: npm
comments: true
highlight_shrink: false
cover: /img/post/64aa2990d4a14c4ca420b3dd4a39a8c8.jpg
abbrlink: 3d6f
date: 2022-11-08 00:00:00
updated:
---

## npm 更改镜像源

### 查看当前的下载源
```shell
npm config get registry
```

### 更改镜像源
```shell
// 淘宝镜像源
npm config set registry https://registry.npmmirror.com/
```

### 镜像源
```text
// 淘宝镜像源
registry=https://registry.npmmirror.com/
```