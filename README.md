# 我的博客

这是一个使用 Jekyll 搭建并托管在 GitHub Pages 上的个人博客。

## 博客地址

访问 [https://jxlwqq.github.io](https://jxlwqq.github.io) 查看博客。

## 本地运行

1. 安装依赖：
```bash
bundle install
```

2. 启动本地服务器：
```bash
bundle exec jekyll serve
```

3. 在浏览器中访问 `http://localhost:4000`

## 写文章

1. 在 `_posts` 目录下创建新文件
2. 文件名格式：`YYYY-MM-DD-title.md`
3. 添加 Front Matter：

```yaml
---
layout: post
title: "文章标题"
date: 2025-12-05 10:00:00 +0800
categories: category1 category2
---
```

4. 使用 Markdown 编写文章内容

## 部署

将代码推送到 GitHub 仓库的 `master` 或 `main` 分支，GitHub Pages 会自动构建和部署。

## 技术栈

- Jekyll - 静态网站生成器
- GitHub Pages - 免费托管
- Markdown - 文章编写
- Minima - 默认主题

## License

MIT
