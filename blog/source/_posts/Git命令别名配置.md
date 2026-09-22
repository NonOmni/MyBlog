---
title: Git 命令别名配置
date: 2024-12-04
categories:
  - Git
tags:
  - git
---

## 将 Git 命令进行简化

### 使用命令行修改 Git 指令

```bash
git config --global alias.st status
```

`--global` 参数是全局参数，也就是这些命令在这台电脑的所有 Git 仓库下都有用。

## 配置文件

每个仓库的 Git 配置文件都放在 `.git/config` 文件中：

```
$ cat .git/config
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[remote "origin"]
    url = git@github.com:michaelliao/learngit.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
[alias]
    last = log -1
```

别名就在 `[alias]` 后面，要删除别名，直接把对应的行删掉即可。

当前用户的 Git 配置文件放在用户主目录下的一个隐藏文件 `.gitconfig` 中：

```
$ cat .gitconfig
[alias]
    co = checkout
    ci = commit
    br = branch
    st = status
[user]
    name = Your Name
    email = your@email.com
```

配置别名也可以直接修改这个文件，如果改错了，可以删掉文件重新通过命令配置。
