# AGENTS.md

这是一个基于 Jekyll 的个人博客项目，托管在 GitHub Pages 上。

## 项目概述

- **类型**: 静态博客网站
- **框架**: Jekyll
- **托管**: GitHub Pages
- **主题**: 基于 Poole 定制
- **仓库**: https://github.com/jxlwqq/jxlwqq.github.io
- **网站**: https://jxlwqq.github.io

## 目录结构

```
├── _config.yml      # Jekyll 配置文件
├── _posts/          # 博客文章目录
├── _layouts/        # 页面布局模板
├── _includes/       # 可复用的 HTML 片段
├── _sass/           # Sass 样式文件
├── _site/           # 生成的静态网站（不要手动编辑）
├── assets/          # 静态资源（图片等）
├── Gemfile          # Ruby 依赖管理
├── index.md         # 首页
└── about.md         # 关于页面
```

## 开发环境设置

### 前置要求

- Ruby (推荐使用 rbenv 管理版本)
- Bundler

### 安装依赖

```bash
eval "$(rbenv init -)" && bundle install
```

### 启动本地开发服务器

```bash
eval "$(rbenv init -)" && bundle exec jekyll serve
```

服务器启动后访问 `http://localhost:4000`

### 如果端口被占用

```bash
lsof -ti:4000 | xargs kill -9 2>/dev/null || true
eval "$(rbenv init -)" && bundle exec jekyll serve
```

## 写作指南

### 创建新文章

1. 在 `_posts/` 目录下创建文件
2. 文件名格式: `YYYY-MM-DD-title.md`
3. 添加 Front Matter:

```yaml
---
layout: post
title: "文章标题"
date: YYYY-MM-DD HH:MM:SS +0800
categories: category1 category2
---
```

### 图片资源

- 图片存放在 `assets/images/` 目录下
- 按文章组织图片，例如: `assets/images/article-name/`
- Markdown 引用格式: `![alt](/assets/images/article-name/image.png)`

## 代码规范

### Front Matter

- `layout`: 必需，通常为 `post` 或 `page`
- `title`: 必需，文章标题
- `date`: 必需，发布日期和时区
- `categories`: 可选，用空格分隔的分类列表

### Markdown

- 使用 kramdown 作为 Markdown 解析器
- 支持 GFM (GitHub Flavored Markdown) 语法
- 代码块使用三个反引号包裹，并指定语言

### 样式

- 样式文件位于 `_sass/` 目录
- 主样式入口: `styles.scss`
- 使用 Sass 变量定义在 `_sass/_variables.scss`

## 部署

- 将代码推送到 `master` 分支
- GitHub Pages 会自动构建和部署
- 不需要手动构建 `_site/` 目录

## 注意事项

- 不要直接编辑 `_site/` 目录中的文件，它们是自动生成的
- 修改 `_config.yml` 后需要重启开发服务器
- 图片文件名避免使用中文和特殊字符
- 文章文件名使用小写字母和连字符

## 常用插件

项目使用以下 Jekyll 插件:

- `jekyll-feed` - RSS 订阅
- `jekyll-seo-tag` - SEO 优化
- `jekyll-paginate` - 分页
- `jekyll-gist` - GitHub Gist 嵌入
