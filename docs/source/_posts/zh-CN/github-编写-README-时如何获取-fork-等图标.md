---
title: github 编写 README 时如何获取 fork 等图标
top: false # 推荐文章（文章是否置顶）
cover: true # 表示该文章是否需要加入到首页轮播封面中
toc: true
lang: zh-CN
tags: [README, 开源项目]
categories: 项目
abbrlink: f7c6a6b8
date: 2019-09-02 23:25:07
password:
summary: 在 Github 自述文档添加 fork 等动态图标。
---

一般比较正式的开源项目会在 `README.md` 的开头添加类似如下图标：

<p align="center"> 
<a href="https://xinetzone.github.io" target="_blank" rel="noopener noreferrer"><img width="100" src="https://xinetzone.github.io/favicon.png" alt="Blog logo"></a>
</p>

<p align="center">
<a href="https://www.gnu.org/licenses/"><img src="https://img.shields.io/github/license/xinetzone/xinetzone.github.io.svg" alt="License"></a>
<a href="http://hits.dwyl.io/xinetzone/xinetzonegithubio"><img src="http://hits.dwyl.io/xinetzone/xinetzonegithubio.svg" alt="HitCount"></a>
<a href="https://github.com/xinetzone/xinetzone.github.io/network"><img src="https://img.shields.io/github/forks/xinetzone/xinetzone.github.io.svg" alt="GitHub forks"></a> <a href="https://github.com/xinetzone/xinetzone.github.io/stargazers"><img src="https://img.shields.io/github/stars/xinetzone/xinetzone.github.io.svg" alt="GitHub stars"></a>
</p>

那么该如何生成上面的图标效果呢？首先，我们可以借由 <http://hits.dwyl.io/> 网站来获取 `hits` 数：

![hits](hits.png)

只需要修改

```
[![HitCount](http://hits.dwyl.io/xinetzone/xinetzonegithubio.svg)](http://hits.dwyl.io/xinetzone/xinetzonegithubio)
```

为

```
<a href="http://hits.dwyl.io/xinetzone/xinetzonegithubio">
<img src="http://hits.dwyl.io/xinetzone/xinetzonegithubio.svg" alt="HitCount"></a>
```

`licenses` 可以这样写：

```
<a href="https://www.gnu.org/licenses/">
<img src="https://img.shields.io/github/license/xinetzone/xinetzone.github.io.svg" alt="License"></a>
```

同样 fork 与 star 可以这样写：

```
<a href="https://github.com/xinetzone/xinetzone.github.io/network">
<img src="https://img.shields.io/github/forks/xinetzone/xinetzone.github.io.svg" alt="GitHub forks"></a> 
<a href="https://github.com/xinetzone/xinetzone.github.io/stargazers">
<img src="https://img.shields.io/github/stars/xinetzone/xinetzone.github.io.svg" alt="GitHub stars"></a>
```

通过这里例子，大家应该看出规律了：针对 `fork`、`star` 只需要将 `xinetzone` 替换为个人 github 账户即可。而 `licenses` 只需要修改 `href` 为对应的 `licenses` 类型即可。

那最开头的图片如何得到？代码很简单：

```
<p align="center">
<a href="https://xinetzone.github.io" target="_blank" rel="noopener noreferrer"><img width="100" src="https://xinetzone.github.io/favicon.png" alt="Blog logo"></a>
</p>
```

`href` 替换为 GitHub Pages 创建的博客 host。

最终，完整的代码为：

```
<p align="center">
<a href="https://xinetzone.github.io" target="_blank" rel="noopener noreferrer"><img width="100" src="https://xinetzone.github.io/favicon.png" alt="Blog logo"></a>
</p>

<p align="center">
<a href="https://www.gnu.org/licenses/"><img src="https://img.shields.io/github/license/xinetzone/xinetzone.github.io.svg" alt="License"></a>
<a href="http://hits.dwyl.io/xinetzone/xinetzonegithubio"><img src="http://hits.dwyl.io/xinetzone/xinetzonegithubio.svg" alt="HitCount"></a>
<a href="https://github.com/xinetzone/xinetzone.github.io/network"><img src="https://img.shields.io/github/forks/xinetzone/xinetzone.github.io.svg" alt="GitHub forks"></a> <a href="https://github.com/xinetzone/xinetzone.github.io/stargazers"><img src="https://img.shields.io/github/stars/xinetzone/xinetzone.github.io.svg" alt="GitHub stars"></a>
</p>
```