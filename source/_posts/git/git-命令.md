---
title: git 命令
categories: git
comments: true
highlight_shrink: false
cover: /img/post/1c81fbb7752647b382f51327fd80f04a.png
abbrlink: dbab
date: 2022-11-08 00:00:00
updated:
---

## git 命令
### 忽略校验提交
```git
git commit --no-verify -m "提交信息"
```
### 删除远程仓库分支
```git
git push origin --delete remoteBranchName
```

### 克隆分支
```git
git clone -b develop giturl
```