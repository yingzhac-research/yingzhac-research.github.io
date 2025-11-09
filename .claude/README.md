# Claude Skills for Blog Writing

这个目录包含了为本博客项目定制的 Claude Code Skills。

## 可用 Skills

### 📝 Blog Writing Assistant

**文件：** `skills/blog-writing-assistant.md`

**用途：** 帮助编写包含数学公式的博客文章，自动检测和修复 Markdown 与 LaTeX 渲染冲突。

**如何使用：**

在 Claude Code 中，你可以通过以下方式调用这个 skill：

```
请使用 blog-writing-assistant 检查我的文章
```

或者在写作过程中：

```
帮我检查这个公式是否会有渲染问题：$|x - x_0| < \delta$
```

**主要功能：**

1. **自动检测冲突**
   - 管道符 `|` 与表格语法冲突
   - 大于/小于号与引用块冲突
   - 多个行内公式的复杂场景

2. **提供修复建议**
   - 推荐使用块级公式 `$$...$$`
   - 提供具体的修改代码
   - 解释为什么需要修改

3. **最佳实践指导**
   - 何时使用行内公式
   - 何时使用块级公式
   - 标准修复模板

4. **发布前检查**
   - 快速检查清单
   - 确保 `math: true` 设置
   - 验证所有公式正确性

## 使用场景

### 场景 1：写新文章前

```
我要写一篇关于微积分的文章，帮我确保公式格式正确
```

### 场景 2：修复现有文章

```
检查 _posts/2025-11-08-calculus-basics-test.md 的公式
```

### 场景 3：实时检查

在写作过程中，随时询问：

```
这个公式会有问题吗？对于任意 $\epsilon > 0$，存在 $\delta > 0$...
```

## 相关文档

- **详细指南：** `docs/markdown-latex-guide.md`
- **Chirpy 主题文档：** https://chirpy.cotes.page/

## 贡献

如果你发现新的 Markdown-LaTeX 冲突场景，欢迎更新 skill 文件或创建新的 skill。

---

**提示：** 这些 skills 是项目特定的，存储在项目仓库中，方便团队协作和知识共享。
