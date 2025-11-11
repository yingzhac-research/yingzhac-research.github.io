---
title: 概率论与统计学基础
date: 2025-11-07 14:00:00 +0800
categories: [Mathematics, Probability]
tags: [probability, statistics, mathematics, test]
math: true
---

这是第二篇测试博客文章，用于测试LaTeX公式渲染和深色主题的文字亮度。

## 概率论基础

### 概率的定义

对于样本空间 $\Omega$ 和事件 $A$，概率定义为：

$$
P(A) = \frac{\text{有利结果数}}{\text{总结果数}}
$$

其中 $0 \leq P(A) \leq 1$，且：

$$
P(\Omega) = 1, \quad P(\emptyset) = 0
$$

### 条件概率

给定事件 $B$ 发生的条件下，事件 $A$ 发生的概率为：

$$
P(A|B) = \frac{P(A \cap B)}{P(B)}, \quad P(B) > 0
$$

### 贝叶斯定理

这是概率论中最重要的定理之一：

$$
P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B)}
$$

更一般的形式（全概率公式）：

$$
P(A|B) = \frac{P(B|A) \cdot P(A)}{\sum_{i=1}^{n} P(B|A_i) \cdot P(A_i)}
$$

## 随机变量

### 期望值

离散随机变量 $X$ 的期望值定义为：

$$
E[X] = \sum_{i=1}^{n} x_i \cdot P(X = x_i)
$$

连续随机变量的期望值：

$$
E[X] = \int_{-\infty}^{\infty} x \cdot f(x) \, dx
$$

其中 $f(x)$ 是概率密度函数。

### 方差

方差衡量随机变量的离散程度：

$$
\text{Var}(X) = E[(X - E[X])^2] = E[X^2] - (E[X])^2
$$

标准差为：

$$
\sigma = \sqrt{\text{Var}(X)}
$$

## 常见分布

### 正态分布（高斯分布）

这是统计学中最重要的分布：

$$
f(x) = \frac{1}{\sigma\sqrt{2\pi}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)
$$

其中：
- $\mu$ 是均值
- $\sigma^2$ 是方差

标准正态分布（$\mu = 0, \sigma = 1$）：

$$
\phi(x) = \frac{1}{\sqrt{2\pi}} e^{-\frac{x^2}{2}}
$$

### 二项分布

$n$ 次独立重复试验中成功 $k$ 次的概率：

$$
P(X = k) = \binom{n}{k} p^k (1-p)^{n-k}
$$

其中组合数定义为：

$$
\binom{n}{k} = \frac{n!}{k!(n-k)!}
$$

### 泊松分布

适用于稀有事件的分布：

$$
P(X = k) = \frac{\lambda^k e^{-\lambda}}{k!}
$$

其中 $\lambda$ 是单位时间内事件发生的平均次数。

## 大数定律与中心极限定理

### 大数定律

样本均值收敛到期望值：

$$
\lim_{n \to \infty} P\left(\left|\frac{1}{n}\sum_{i=1}^{n} X_i - \mu\right| < \epsilon\right) = 1
$$

### 中心极限定理

独立同分布随机变量之和的分布趋向于正态分布：

$$
\frac{\sum_{i=1}^{n} X_i - n\mu}{\sigma\sqrt{n}} \xrightarrow{d} N(0, 1)
$$

其中 $\xrightarrow{d}$ 表示依分布收敛。

## 假设检验

### Z-检验统计量

对于正态总体，检验统计量为：

$$
Z = \frac{\bar{X} - \mu_0}{\sigma / \sqrt{n}}
$$

### t-检验统计量

当总体方差未知时：

$$
t = \frac{\bar{X} - \mu_0}{s / \sqrt{n}}
$$

其中 $s$ 是样本标准差：

$$
s = \sqrt{\frac{1}{n-1}\sum_{i=1}^{n}(X_i - \bar{X})^2}
$$

### 置信区间

均值的 $(1-\alpha)$ 置信区间为：

$$
\left[\bar{X} - z_{\alpha/2}\frac{\sigma}{\sqrt{n}}, \quad \bar{X} + z_{\alpha/2}\frac{\sigma}{\sqrt{n}}\right]
$$

## 线性回归

### 最小二乘法

寻找最佳拟合直线 $y = \beta_0 + \beta_1 x$：

$$
\min_{\beta_0, \beta_1} \sum_{i=1}^{n} (y_i - \beta_0 - \beta_1 x_i)^2
$$

解为：

$$
\beta_1 = \frac{\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y})}{\sum_{i=1}^{n}(x_i - \bar{x})^2}
$$

$$
\beta_0 = \bar{y} - \beta_1\bar{x}
$$

### 决定系数 R²

衡量模型拟合优度：

$$
R^2 = 1 - \frac{\sum_{i=1}^{n}(y_i - \hat{y}_i)^2}{\sum_{i=1}^{n}(y_i - \bar{y})^2}
$$

其中 $\hat{y}_i$ 是预测值。

## 协方差与相关系数

### 协方差

衡量两个随机变量的线性相关程度：

$$
\text{Cov}(X, Y) = E[(X - E[X])(Y - E[Y])]
$$

### 皮尔逊相关系数

标准化的协方差：

$$
\rho_{X,Y} = \frac{\text{Cov}(X, Y)}{\sigma_X \sigma_Y}
$$

其中 $-1 \leq \rho \leq 1$。

## 矩母函数

随机变量 $X$ 的矩母函数定义为：

$$
M_X(t) = E[e^{tX}] = \int_{-\infty}^{\infty} e^{tx} f(x) \, dx
$$

第 $n$ 阶矩可以通过求导得到：

$$
E[X^n] = \left.\frac{d^n M_X(t)}{dt^n}\right|_{t=0}
$$

## 信息论

### 熵

衡量随机变量的不确定性：

$$
H(X) = -\sum_{i=1}^{n} P(x_i) \log_2 P(x_i)
$$

### KL散度

衡量两个概率分布的差异：

$$
D_{KL}(P \parallel Q) = \sum_{i} P(x_i) \log\frac{P(x_i)}{Q(x_i)}
$$

## 结论

这篇文章测试了：
- ✅ 各种概率统计公式的LaTeX渲染
- ✅ 复杂的数学符号（求和、积分、极限）
- ✅ 分式、指数、根号等表达式
- ✅ 深色主题下的文字亮度和可读性

希望文字现在足够亮，阅读起来更舒适！
