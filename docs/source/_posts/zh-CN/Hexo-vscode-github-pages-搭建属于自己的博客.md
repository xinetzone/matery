---
title: Hexo+vscode+github pages 搭建属于自己的博客
top: false
cover: false
toc: true
lang: zh-CN
tags: [github pages, hexo]
categories: 教程
abbrlink: 41cccb40
date: 2019-09-02 14:34:07
password:
summary: 利用 hexo-theme-matery 借由 vscode 与 Github Pages 搭建属于自己的博客。
---

参考：[超详细Hexo+Github博客搭建小白教程](https://godweiyang.com/2018/04/13/hexo-blog/#toc-heading-1/)

Hexo 是高效的静态站点生成框架，它基于 `Node.js`。通过 Hexo，你可以直接使用 Markdown 语法来撰写博客。本文搭建的环境是 Windows10。

## 安装 Node.js

首先下载稳定版 Node.js：<https://nodejs.org/en/download/>。
安装选项全部默认，一路点击 `Next`。

在 Windows PowerShell 中输入：

```sh
$ node -v
$ npm -v
```

如果没有报错，便说明安装成功。

## 安装 Git 与 vscode

为了把本地的网页文件上传到 github 上面去，我们需要用到分布式版本控制工具：Git[下载地址](https://git-scm.com/download/win)。安装选项还是全部默认，只不过最后一步添加路径时选择 `Use Git from the Windows Command Prompt`，这样我们就可以直接在命令提示符里打开 git 了。安装完成后在命令提示符中输入 `git --version` 验证是否安装成功。

[vscode](https://code.visualstudio.com/) 的安装便比较简单，直接按照提示安装即可。

## 创建 GitHub Pages

在你的 GitHub 主页打开如下界面：

![创建 repo](1114626-aa71be3d8b914371.png)

然后如下图所示，输入自己的项目名字，后面一定要加 `.github.io` 后缀，`README`初始化也要勾上。名称一定要和你的github名字完全一样，比如你 `github` 名字叫`abc`，那么仓库名字一定要是 `abc.github.io`。

![](1114626-f796295247fb7aba.png)

然后项目就建成了，点击 `Settings`，向下拉到最后有个 `GitHub Pages`，点击 `Choose a theme` 选择一个主题。将 `GitHub Pages` 生成的网址复制到如下位置：

![](1114626-ae9a9d173799c870.png)

点击网址 <https://xinetzone.github.io/>，便会显示：

![](1114626-93636579128421e5.png)

此页面的内容是由 [xinetzone](https://github.com/xinetzone)/**[xinetzone.github.io](https://github.com/xinetzone/xinetzone.github.io)** 根目录的 `README.md` 提供的。

![](1114626-97cfccb76ec79543.png)

使用 vscode 打开本地的一个文件夹：

![](1114626-2126a847e377b804.png)

选择 Git Bash 作为默认：

![](1114626-f0f238bc6f947912.png)

![](1114626-a3e18c31da2eeb5a.png)

为了提高 npm 运行速度需要添加淘宝源：

```sh
 $ npm config set registry https://registry.npm.taobao.org
```

运行如下命令安装 hexo：

```sh
$ npm i hexo-cli -g
```

安装完后输入 `hexo -v` 验证是否安装成功。将你在 GitHub 上的 reop 克隆至本地，并切换到 hexo 分支（用于存放网站的源代码）：

```sh
$ git clone https://github.com/xinetzone/xinetzone.github.io.git
$ cd xinetzone.github.io/
$ git checkout hexo
```

创建一个目录用于存储博客文件，切换目录并初始化网站：

```sh
$ mkdir docs
$ cd docs/
$ hexo init
$ npm install
```

其中 `hexo init` 为网站初始化环境，`npm install` 安装必备的组件，我们可以看到 `blog` 目录下生成如下目录：

![](1114626-f1260417e24c3632.png)

- `node_modules`: 依赖包
- `public`：存放生成的页面，运行 `hexo g` 便会生成，而 `hexo clean` 便会删除
- `scaffolds`：生成文章的一些模板
- `source`：用来存放你的文章
- `themes`：主题
- `_config.yml`: 博客的配置文件

这样本地的网站配置也弄好啦，输入 `hexo g` 生成静态网页，然后输入 `hexo s` （hexo serve）打开本地服务器：

![](1114626-77606c3fdfd2f043.png)

这样便可以在 `http://localhost:4000` 预览网站了：

![](1114626-3de8c569ca663fec.png)

使用 `Ctrl + C` 可以把服务关掉。

## 将 hexo 与 github 关联起来

首先输入如下命令，配置 Git 的环境：

```sh
$ git config --global user.name  xinetzone
$ git config --global user.email xinzone@outlook.com
```

用户名和邮箱根据你注册 github 的信息自行修改。然后生成密钥 SSH key：

```sh
$ ssh-keygen -t rsa -C "xinzone@outlook.com"
```

查看 `id_rsa.pub`：

```sh
$ cat ~/.ssh/id_rsa.pub
```

打开你自己的 github，在头像下面点击 `settings`，再点击 `SSH and GPG keys`，新建一个SSH，名字随便，然后将 `id_rsa.pub` 复制粘贴到指定位置。在 git bash中，查看是否成功：

```sh
$ ssh -T git@github.com
```

打开博客根目录下的 `_config.yml` 文件，这是博客的配置文件，在这里你可以修改与博客相关的各种信息。

将 hexo 部署到 GitHub 修改最后一行的配置：

```sh
deploy:
  type: git
  repository: https://github.com/xinetzone/xinetzone.github.io.git
  branch: master 
```

其中  `repository` 可以通过如下方法获取：

![](1114626-890059e5643e50f7.png)

`repository` 修改为你自己的 github 项目地址。接着需要先安装 `deploy-git`，也就是部署的命令，这样你才能用命令部署到 GitHub。接着 `hexo clean` 清除了你之前生成的东西，也可以不加。 `hexo g` 顾名思义，生成静态文章是 `hexo generate` 的缩写 `hexo deploy` 部署文章，可以用 `hexo d` 缩写：

```sh
$ npm install hexo-deployer-git --save
$ hexo clean | hexo g | hexo d
```

这时打开你的 github.io（<https://xinetzone.github.io/>） 主页就能看到发布的文章：

![](1114626-761726a5770eea11.png)

为了添加博客，需要：

```sh
$ hexo new post "博客名"
```

然后打开 `blog\source\_posts` 的目录，可以发现下面多了一个文件夹和一个 `.md` 文件，一个用来存放你的图片等数据，另一个就是你的文章文件啦。

## 备份博客源文件

将本地的 `hexo` 分支推送到远程：

```sh
$ git add .
$ git commit -m "hexo init"
$ git push origin hexo
```

## 自定义博客的个人信息

首先删除 hexo 自动生成的 `docs/source/_posts/hello-world.md` 文档，然后使用如下命令创建属于自己的博客，比如：

```sh
$ cd docs
$ hexo new post "Hexo + vscode + github pages 搭建属于自己的博客"
```

这样便会在目录 `docs/source/_posts/` 下面生成 `Hexo-vscode-github-pages-搭建属于自己的博客.md` 文档，接着只需要在此文档中填充内容即可。在文章开头可以配置文档的布局：

```
---
title: Hexo + vscode + github pages 搭建属于自己的博客
date: 2019-09-01 19:37:09
categories: 教程 #文章文类
tags: [hexo, github] #文章标签，多于一项时用这种格式
---
```

## 修改 `_config.yml` 匹配个人需求

```yml
# Site
title: 刘新伟的技术博客专栏 # 标题
subtitle: # 子标题
description: # 站点描述，给搜索引擎看的
keywords: # 关键字
author: 刘新伟
language: zh-CN
timezone: Asia/Shanghai # 时区
```

其中，`description` 主要用于 SEO，告诉搜索引擎一个关于您站点的简单描述，通常建议在其中包含您网站的关键词。`author` 参数用于主题显示文章的作者。

为了博客可以支持图片的上传需要修改 `_config.yml`：

```yml
post_asset_folder: true # true 支持图片本地上传
```

如果你的 Hexo 项目中只有少量图片，那最简单的方法就是将它们放在 `/docs/source/images` 文件夹中。然后通过类似于 `![](/images/image.jpg)`的方法访问它们，详细内容参考[资源文件夹](https://hexo.io/zh-cn/docs/asset-folders.html)。

通过常规的 markdown 语法和相对路径来引用图片和其它资源可能会导致它们在存档页或者主页上显示不正确。随着 Hexo 3 的发布，许多新的标签插件被加入到了核心代码中。这使得你可以更简单地在文章中引用你的资源。

```markdown
{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}
```

设置好之后便可以正常显示结果：

![](2019-09-01-170438.png)

可以看出，此时的标题与字体均发生了改变。

**注意**：`{% asset_img slug [title] %}` 中的 `title` 不可以为空值，如果想要省略，可以这样：`{% asset_img slug  %}`，即使用空格代替 `title`（注意 `slug` 后面有两个空格）。

如果在执行 `hexo deploy` 后,出现 error deployer not found:github 的错误，请执行：

```sh
$ npm install hexo-deployer-git --save
```

如果您觉得麻烦，可以直接 fork 我已经配置好的博客模板 [xinetzone-matery](https://github.com/xinetzone/xinetzone.github.io) 并按照 README 进行操作即可。