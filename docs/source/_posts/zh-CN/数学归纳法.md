---
title: 数学归纳法
top: false
cover: false
toc: true
comments: true
lang: zh-CN
summary: 数学归纳法简介
tags: 数学归纳法
categories: 数学
abbrlink: '886e6229'
date: 2020-02-14 10:14:03
password:
---

## 1. 第一数学归纳法

设 $P(n)$ 表示一个与自然数 $n$ 有关的命题，若

1. $P(n_0)$（$n_0 \in \mathbb{N}$）成立；
2. 假设 $P(k)$（$k\geq n_0$）成立，可推出 $P(k+1)$ 成立，

则 $P(n)$ 对一切自然数 $n\ge n_0$，$n\in \mathbb{N}$ 都成立。

## 2. 第二数学归纳法

设 $P(n)$ 表示一个与自然数 $n$ 有关的命题，若

1. $P(n_0)$（$n_0 \in \mathbb{N}$）成立；
2. 假设 $P(n)$ 在 $n_0 \le n \le k$ 时成立，可推出 $P(k+1)$ 成立，

则 $P(n)$ 对一切自然数 $n\ge n_0$，$n\in \mathbb{N}$ 时都成立。

## 3. 逆向归纳法（亦称倒推归纳法或向前-向后归纳法）

- 第 1 步：运用通常的归纳法证明命题 $P(n)$ 对自然数的某个子序列  $\{n_k\}$ 成立，即 $P(n_k)$ 成立（$n_k \to + \infty$）.
- 第 2 步：$P(n)$ 成立可以推出 $P(n-1)$ 成立，

则对于一切自然数 $n$，$P(n)$ 成立.

例题1：设 $a_1, a_2, \cdots, a_n \in \mathbb{R}^+$，$A_n = \frac{1}{n} (a_1 + a_2 + \cdots + a_n)$，$G_n = \sqrt[^n]{(a_1a_2\cdots a_n)}$，求证：$A_n \geq G_n$ （等号成立当且仅当 $a_1=a_2=\cdots = a_n$ 时成立）。

【证明】先证对一切 $n = 2^m$（$m \in \mathbb{N}$），$A_n \geq G_n$ 成立，为此对 $m$ 使用归纳法。

当 $m=1$ 时，有：

$$
A_2 = \frac{1}{2} (a_1 + a_2) = \frac{1}{2} (\sqrt{a_1} - \sqrt{a_2})^2 + \sqrt{a_1a_2} \geq \sqrt{a_1a_2} = G_2
$$

等号当且仅当 $a_1 = a_2$ 时成立。即 $m=1$ 时，$A_{2^m} \geq G_{2^m}$ 成立。

假设当 $m=k \in \mathbb{N}$ 时，不等式成立，即 $A_{2^k} \geq G_{2^k}$。于是，当 $m = k+1$ 时有：

$$
\begin{aligned}
A_{2^{k+1}} &= \frac{1}{2^{k+1}} (a_1 +a_2+\cdots + a_{2^{k+1}})\\
&= \frac{1}{2} \cdot \frac{1}{2^{k}}\left[(a_1 + \cdots + a_{2^k}) + (a_{2^k+1} + \cdots + a_{2^{k+1}})\right]\\
&\geq \frac 1 2 (\sqrt[2^k] {a_1\ldots a_{2^k}} + \sqrt[2^k] {a_{2^k+1}\ldots a_{2^{k+1}}})\\
&\geq \sqrt[2^{k+1}] {a_1\ldots a_{2^k}a_{2^k+1}\ldots a_{2^{k+1}}}
= G_{2^{k+1}}
\end{aligned}
$$

所以，对一切 $n=2^m$ ($m=1,2,\cdots$)，$A_{2^m} \geq G_{2^m}$ 成立。接着证明，如果对于任意的 $k \in \mathbb{N}$，$A_k \ge G_k$ 成立，那么 $A_{k-1} \ge G_{k-1}$ 也成立。

事实上，我们令 $a_k = \frac 1 {k-1} (a_1 + a_2 + \ldots + a_{k-1})$，则

$$
\begin{aligned}
A_{k-1} &= a_k = \frac{(k-1)(a_k) + a_k}{k} \\
&= \frac 1 k (a_1 + a_2 + \ldots + a_k)\\
&\ge \sqrt[k]{a_1\ldots a_{k-1} \cdot a_k}
\end{aligned}
$$

故而 $A_{k-1}^k \ge (G_{k-1})^{k-1} A_{k-1}$，即 $A_{k-1} \ge G_{k-1}$ 成立。

由逆向归纳法知，命题成立。

## 4 跳跃数学归纳法

设 $P(n)$ 表示一个与自然数 $n$ 有关的命题，若

1. $P(m)$（$1\le m \le t$）成立；
2. 假设 $P(k)$ 成立，可推出 $P(k+t)$ 成立，

则 $P(n)$ 对一切自然数 $n$ 都成立。

## 5 螺旋归纳法

设 $P(n)$  和 $Q(n)$ 是两串与自然数 $n$ 有关的命题，如果

(1) 命题 $P(1)$ 成立；
(2) 对于 $k \in \mathbb{N}$，若命题 $P(k)$ 成立，则命题 $Q(k)$ 成立，若命题 $Q(k)$ 成立，则命题 $P(k+1)$ 成立，

则对于所有自然数 $n$，命题 $P(n)$ 与 $Q(n)$ 都成立.

