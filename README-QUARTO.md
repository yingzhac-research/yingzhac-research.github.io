# Quarto 博客迁移说明

本仓库已从 Jekyll (Chirpy 主题) 迁移到 Quarto。

## 为什么迁移到 Quarto？

1. **LaTeX 支持更好** - 原生支持，无需额外配置
2. **深色主题问题解决** - Darkly 主题开箱即用，对比度高
3. **多格式输出** - 同一份文章可以输出为：
   - HTML (网页博客)
   - PDF (论文/书籍章节)
   - Word 文档
   - 演示文稿
4. **学术功能完整** - 支持引用管理、交叉引用、定理环境等
5. **未来可扩展** - 可以无缝扩展为书籍或教材

## 项目结构

```
.
├── _quarto.yml           # Quarto 主配置文件
├── index.qmd            # 首页
├── posts.qmd            # 博客列表页
├── about.qmd            # 关于页面
├── posts/               # 博客文章目录
│   ├── 2025-11-08-calculus-basics-test.qmd
│   └── 2025-11-07-probability-statistics-basics.qmd
├── styles.css           # 自定义样式（深色主题优化）
├── references.bib       # 参考文献数据库
├── .claude/             # Claude Code Skills (保留)
├── docs/                # 文档 (保留)
└── .github/workflows/
    └── quarto-publish.yml  # GitHub Actions 部署配置
```

## 本地预览

```bash
# 安装 Quarto
# 参见：https://quarto.org/docs/get-started/

# 预览网站
quarto preview

# 构建网站
quarto render
```

## 写新文章

1. 在 `posts/` 目录创建新的 `.qmd` 文件
2. 文件名格式：`YYYY-MM-DD-title.qmd`
3. Front matter 格式：

```yaml
---
title: "文章标题"
author: "Research Blog"
date: "YYYY-MM-DD"
categories: [Category1, Category2]
description: "文章描述"
draft: false
---

文章内容...
```

## 数学公式

行内公式：`$E = mc^2$`

块级公式：
```
$$
\int_a^b f(x) \, dx
$$
```

**注意：** Quarto 原生支持 LaTeX，无需额外配置 `math: true`

## 导出为 PDF

任何文章都可以导出为 PDF：

```bash
quarto render posts/2025-11-08-calculus-basics-test.qmd --to pdf
```

## 迁移历史

- **2025-11-09**: 从 Jekyll Chirpy 迁移到 Quarto
- 保留了所有现有文章
- 保留了 Claude Skills 和文档
- 解决了深色主题文字对比度问题

## 参考资源

- [Quarto 官方文档](https://quarto.org/)
- [Quarto 博客指南](https://quarto.org/docs/websites/website-blog.html)
- [Markdown-LaTeX 兼容性指南](docs/markdown-latex-guide.md)
- [博客写作助手 Skill](.claude/skills/blog-writing-assistant.md)
