# Markdown 与 LaTeX 兼容性指南

本文档记录在 Jekyll + Chirpy 博客中编写数学公式时遇到的 Markdown 和 LaTeX 冲突问题及解决方案。

## 目录

- [问题背景](#问题背景)
- [常见冲突](#常见冲突)
- [解决方案](#解决方案)
- [最佳实践](#最佳实践)
- [示例](#示例)

---

## 问题背景

Markdown 和 LaTeX 都使用一些相同的特殊字符，但含义不同。在 Jekyll 处理博客文章时：

1. **Markdown 解析器先运行**（识别 Markdown 语法）
2. **LaTeX 引擎后运行**（渲染数学公式）

这导致 Markdown 解析器可能"破坏"LaTeX 代码，使公式无法正确渲染。

### 处理流程

```
原始文本
    ↓
Markdown 解析器（识别 |, >, *, _ 等）
    ↓
HTML + LaTeX 标记
    ↓
MathJax/KaTeX 渲染引擎（处理 $...$ 和 $$...$$）
    ↓
最终显示
```

---

## 常见冲突

### 1. 管道符号 `|` 冲突

**问题：** 在 Markdown 中，`|` 是表格分隔符

```markdown
❌ 错误示例：
当 $0 < |x - x_0| < \delta$ 时，有 $|f(x) - L| < \epsilon$

结果：公式被打断，渲染失败
```

**原因：** Markdown 解析器将 `|` 误认为表格语法。

---

### 2. 大于号 `>` 冲突

**问题：** 在 Markdown 中，行首的 `>` 是引用块标记

```markdown
❌ 错误示例：
对于任意 $\epsilon > 0$，存在 $\delta > 0$

结果：$\epsilon 和 $\delta 无法正确渲染
```

**原因：** 某些 Markdown 解析器可能将 `>` 误解析为引用块。

---

### 3. 同一行多个行内公式

**问题：** 一行中包含多个 `$...$` 和特殊字符

```markdown
❌ 错误示例：
当且仅当对于任意 $\epsilon > 0$，存在 $\delta > 0$，使得当 $0 < |x - x_0| < \delta$ 时，有 $|f(x) - L| < \epsilon$。

结果：部分公式丢失或渲染异常
```

**原因：** 多个行内公式 + 特殊字符导致解析混乱。

---

### 4. 其他可能的冲突字符

| 字符 | Markdown 含义 | LaTeX 用途 | 冲突风险 |
|------|--------------|-----------|---------|
| `|` | 表格分隔符 | 绝对值、条件概率 | 高 ⚠️ |
| `>` | 引用块 | 大于号、箭头 | 中 ⚠️ |
| `*` | 斜体/粗体 | 乘号、卷积 | 低 |
| `_` | 斜体/下划线 | 下标 | 低 |
| `[` `]` | 链接 | 矩阵括号 | 低 |

---

## 解决方案

### ✅ 方案 1：使用块级公式（推荐）

将复杂的数学内容放入 `$$...$$` 块中：

```markdown
✅ 正确示例：
当且仅当：

$$
\forall \epsilon > 0, \exists \delta > 0, \text{ 使得 } 0 < |x - x_0| < \delta \implies |f(x) - L| < \epsilon
$$
```

**优点：**
- ✅ 完全避免 Markdown 语法冲突
- ✅ 公式独立成行，更清晰
- ✅ 支持复杂的数学表达式

**为什么有效？**
- `$$...$$` 内的内容完全交给 LaTeX 引擎处理
- Markdown 解析器不会处理块级公式内的特殊字符

---

### 方案 2：使用 LaTeX 替代符号（备选）

用 LaTeX 命令代替特殊字符：

```markdown
✅ 替代方案：
- 绝对值：$\vert x \vert$ 或 $\lvert x \rvert$
- 大于：$\gt$ 代替 $>$
- 小于：$\lt$ 代替 $<$
```

**缺点：**
- ❌ 代码可读性差
- ❌ 维护困难

---

### ❌ 不推荐的方案

**方案 3：使用代码块**
```markdown
对于任意 `$\epsilon > 0$`
```
- 公式不会渲染，只显示纯文本

**方案 4：HTML 实体转义**
```markdown
$\epsilon &gt; 0$
```
- 在某些环境下可能失效

---

## 最佳实践

### 1. 选择合适的公式类型

| 场景 | 使用 | 示例 |
|------|------|------|
| 简单变量、常量 | 行内公式 `$...$` | `$x$`, `$\pi$`, `$E = mc^2$` |
| 包含 `\|` 或 `>` | 块级公式 `$$...$$` | 绝对值、不等式 |
| 复杂表达式 | 块级公式 `$$...$$` | 积分、矩阵、多行推导 |
| 定义、定理 | 块级公式 `$$...$$` | 极限定义、泰勒展开 |

---

### 2. 避免常见错误

**❌ 不要：** 一行中放太多行内公式
```markdown
对于 $a$，$b$，$c$，当 $x > 0$ 且 $|y| < 1$ 时...
```

**✅ 改为：**
```markdown
对于 $a$、$b$、$c$，当以下条件成立时：

$$
x > 0 \quad \text{且} \quad |y| < 1
$$
```

---

### 3. 使用标准数学符号

| 符号 | LaTeX 命令 | 含义 |
|------|-----------|------|
| $\forall$ | `\forall` | 对于所有 |
| $\exists$ | `\exists` | 存在 |
| $\implies$ | `\implies` | 推出/蕴含 |
| $\iff$ | `\iff` | 当且仅当 |
| $\in$ | `\in` | 属于 |
| $\subset$ | `\subset` | 子集 |

使用这些符号可以让公式更专业，同时避免中文和公式混杂。

---

## 示例

### 示例 1：极限定义（修正前后对比）

**❌ 修正前（渲染失败）：**
```markdown
当且仅当对于任意 $\epsilon > 0$，存在 $\delta > 0$，使得当 $0 < |x - x_0| < \delta$ 时，有 $|f(x) - L| < \epsilon$。
```

**问题：**
- 多个行内公式
- 包含 `>` 和 `|` 特殊字符

**✅ 修正后（正常渲染）：**
```markdown
当且仅当：

$$
\forall \epsilon > 0, \exists \delta > 0, \text{ 使得 } 0 < |x - x_0| < \delta \implies |f(x) - L| < \epsilon
$$
```

---

### 示例 2：矩阵（推荐写法）

**✅ 正确写法：**
```markdown
$$
A = \begin{pmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22}
\end{pmatrix}
$$
```

---

### 示例 3：分段函数

**✅ 正确写法：**
```markdown
$$
f(x) = \begin{cases}
x^2 & \text{当 } x \geq 0 \\
-x^2 & \text{当 } x < 0
\end{cases}
$$
```

---

### 示例 4：积分与求和

**✅ 正确写法：**
```markdown
$$
\int_a^b f(x) \, dx = \lim_{n \to \infty} \sum_{i=1}^{n} f(x_i^*) \Delta x
$$
```

---

## 快速检查清单

在发布博客文章前，检查以下内容：

- [ ] 包含 `|` 的公式是否使用块级公式？
- [ ] 包含 `>` 或 `<` 的公式是否使用块级公式？
- [ ] 是否避免了一行中多个行内公式 + 特殊字符？
- [ ] 复杂的数学定义是否使用了块级公式？
- [ ] 文章的 front matter 中是否设置了 `math: true`？

---

## Front Matter 配置

确保文章开头包含数学公式支持：

```yaml
---
title: 文章标题
date: YYYY-MM-DD HH:MM:SS +TTTT
categories: [类别]
tags: [标签]
math: true  # ← 必须启用
---
```

---

## 测试公式渲染

可以在本地或在线工具中测试公式：

- **在线 LaTeX 编辑器：** https://www.latexlive.com/
- **MathJax 演示：** https://www.mathjax.org/#demo
- **KaTeX 演示：** https://katex.org/

---

## 参考资源

- [MathJax 文档](https://docs.mathjax.org/)
- [KaTeX 支持的函数](https://katex.org/docs/supported.html)
- [LaTeX 数学符号](https://oeis.org/wiki/List_of_LaTeX_mathematical_symbols)
- [Chirpy 主题文档](https://chirpy.cotes.page/)

---

## 更新日志

- **2025-11-09：** 初始版本，记录 Markdown 和 LaTeX 冲突问题及解决方案
