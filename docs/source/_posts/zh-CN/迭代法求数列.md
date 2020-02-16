---
title: 迭代法求数列
top: false
cover: false
toc: true
comments: true
lang: zh-CN
tags:
  - 数列
  - 迭代法
categories: 数学
abbrlink: 8d33ba78
date: 2020-01-31 17:12:25
password:
summary:
---

## 迭代法

设 $f(x): M \to M$. 记 

$$f^0(x) = x, f^1(x) = f(x), f^2(x) = f(f(x)), \cdots, f^{n+1}(x) = f(f^n(x))$$

其中的 $n$ 叫做 $f^n(x)$ 的迭代次数。

如果 $f(x)$ 有反函数，可以用 $f^{-1}(x)$ 表示。$f^n(x)$ 的反函数是 $f^{-n}(x)$.

一个十分有用的结论：

如果有一个可逆的函数 $\varphi$，取 $F(x) = \varphi^{-1} \circ f \circ \varphi(x)$，则有

$$
F(F(x)) = \varphi^{-1} \circ f \circ \varphi \circ \varphi^{-1} \circ f \circ \varphi(x) = \varphi^{-1} \circ f^2 \circ \varphi(x)
$$

更一般的 $F^n(x) = \varphi^{-1} \circ f^n \circ \varphi(x)$.

这样一来，便把 $F(x)$ 的 $n$ 次迭代问题转换为 $f(x)$ 的 $n$ 次迭代问题了。由于 $\varphi(x)$ 的取法千变万化，这就能够构造出一系列的函数的迭代问题与数列计算问题。

【例1】设 $F(x) = x + 2\sqrt{x} + 1$，计算 $F^n(x)$.

【解】$F(x) = (\sqrt{x} +1)^2$，取 $\varphi(x) = \sqrt{x}$，则 $\varphi^{-1}(x) = x^2, f(x) = x+1$，则 $F^n(x) = (\sqrt{x} + n)^2$.

【例2】设 $F(x) = \frac{x}{\sqrt{x^2 + c}}$，计算 $F^n(x)$.

【解】观察 $F(x)$ 形似 $f(x) = \frac{x}{x+c}$，故c^k而，我们可以设 $\varphi(x) = x^2$，有 $\varphi^{-1}(x) = \sqrt{x}$. 先求得

$$
f^n(x) = \frac{x}{\sqrt{x^2\sum_{k=0}^{n-1} c^k + c^n}}
$$

则 $F^n(x) = \frac{x}{\sqrt{x^2\sum_{k=0}^{n-1} c^k + c^n}}$.

【例3】有数列 $\{a_n\}$，满足 $a_0 = 2$，$a_{n+1} = \frac{a_n^2}{2a_n - 1}$ ($n\in \mathbb{N}$)，求 $a_n$ 的极限。

【解】令 $F(x) = \frac{x^2}{2x - 1}$，则命题转换为求 $F^n(x)$ 的极限。

$$
F(x) = \frac{x^2}{x^2 - (x - 1)^2} = \frac 1 {1 - (1 - \frac 1 x)^2}
$$

取 $\varphi(x) = 1 - \frac 1 x$，有 $\varphi^{-1}(x) = \frac 1 {1 - x}$，$f(x) = x^2$，于是

$$
F^n(x) = \frac 1 {1 - (1 - \frac 1 x)^{2^n}}
$$

最终

$$
a_n = F^n(2) = \frac 1 {1 - 2^{-2n}}
$$

因而 $\lim\limits_{n\to \infty} a_n = 1$.