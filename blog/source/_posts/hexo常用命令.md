---
title: hexo常用命令
date: 2026-08-16 23:05:04
tags:
    - hexo
categories:
    - 博客
---
Hexo 是一个快速、简洁且高效的静态博客框架。本文整理日常使用中最常用的 Hexo 命令。

## 安装与初始化

```bash
# 全局安装 Hexo CLI
npm install -g hexo-cli

# 初始化博客目录
hexo init blog

# 进入目录并安装依赖
cd blog
npm install
```

## 本地预览

```bash
# 启动本地服务器，默认 http://localhost:4000
hexo server
# 简写
hexo s
# 指定端口
hexo server -p 5000
# 仅使用静态文件
hexo server -s
```

## 新建内容

```bash
# 新建文章（默认布局 post）
hexo new "文章标题"
hexo new post "文章标题"

# 新建草稿
hexo new draft "草稿标题"

# 发布草稿
hexo publish "草稿标题"

# 新建页面（如关于、标签页）
hexo new page about
```

## 生成与部署

```bash
# 生成静态文件到 public/
hexo generate
# 简写
hexo g

# 清理缓存与已生成的文件
hexo clean

# 部署到远端
hexo deploy
# 简写
hexo d

# 常用组合：清理后重新生成并部署
hexo clean && hexo g -d
```

## 其他常用命令

```bash
# 查看 Hexo 版本
hexo version

# 列出站点信息
hexo list page   # 列出页面
hexo list post   # 列出文章
hexo list route  # 列出路由

# 查看帮助
hexo help
```

## 常用参数

| 参数               | 说明           |
| ------------------ | -------------- |
| `-p, --port`     | 指定端口       |
| `-s, --static`   | 仅使用静态文件 |
| `-d, --deploy`   | 生成后立即部署 |
| `-g, --generate` | 部署前先生成   |
| `--draft`        | 显示草稿       |
| `--debug`        | 输出调试信息   |

> 提示：`hexo` 命令需在博客根目录（包含 `_config.yml` 的目录）下执行。
