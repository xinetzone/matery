---
title: 如何修改 hexo-theme-matery 模板
top: false
cover: false
toc: true
lang: zh-CN
tags: [github pages, hexo]
categories: 教程
abbrlink: 3567ebbb
date: 2019-09-02 21:06:59
password:
summary: hexo-theme-matery 主题自定义修改
---

## 修改 `/docs/` 目录下的 `_config.yml`

下面介绍如何修改模板主题：<https://github.com/blinkfox/hexo-theme-matery.git>。

首先，在个人 github 创建一个 repo，比如：[xinetzone](https://github.com/xinetzone)/**[xinetzone.github.io](https://github.com/xinetzone/xinetzone.github.io)**，接着克隆到本地。其中 `xinetzone` 是个人用户名称。为了将设置好的主题上传到 GitHub，需要创建一个分支 `hexo`：

```sh
$ cd xinetzone.github.io
$ git checkout -b hexo
$ mkdir docs
$ cd docs
$ hexo init --no-install
```

其中 `--no-install` 表示使用 hexo 进行初始化并跳过 `npm install`。下面需要切换主题，通过 `git submodule` 添加 hexo-theme-matery 主题：

```sh
$ git submodule add https://github.com/blinkfox/hexo-theme-matery.git themes/hexo-theme-matery
```

如果报报"error: RPC failed; curl 56 OpenSSL SSL_read: SSL_ERROR_SYSCALL, errno 10054"解决方法：

```sh
$ git config http.sslVerify "false"
```

如果再报 "git config http.sslVerify "false"  fatal: not in a git directory"，请执行： 

```sh
$ git config  --globle   http.sslVerify "false"
```

修改 `/docs/` 目录下的 `_config.yml`，下面依照 [hexo-theme-matery/README_CN.md](https://github.com/blinkfox/hexo-theme-matery/blob/develop/README_CN.md) 给出我自己的修改：

```yml
# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
title: 刘新伟的博客
subtitle: "知者乐水，仁者乐山"
description: 温州大学 | 应用数学 | 深度学习
keywords: "MXNet Pytorch TensorFlow 刘新伟 计算机视觉 深度学习"
author: 刘新伟
language: # 多语言支持
- zh-tw
- en
timezone:

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: https://xinetzone.github.io/ # https://xxx.github.io/ 类似于 host 服务器
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:

# Directory
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:

# Writing
new_post_name: :title.md # File name of new posts
default_layout: post
titlecase: false # Transform title into titlecase（首字母大写）
external_link: true # Open external links in new tab
filename_case: 0
render_drafts: false
post_asset_folder: true # 为 true参数后，在建立文件时，Hexo 
                         ## 会自动建立一个与文章同名的文件夹，您可以把与该文章相关的所有资源都放到那个文件夹，如此一来，您便可以更方便的使用资源。
relative_link: false
future: true
highlight: # 默认的不好看，需要禁用
  enable: false
  line_number: false
  auto_detect: false
  tab_replace:
  
# Home page setting
# path: Root path for your blogs index page. (default = '')
# per_page: Posts displayed per page. (0 = disable pagination)
# order_by: Posts order. (Order by date descending by default)
index_generator:
  path: ''
  per_page: 18
  order_by: -date
  
# Category & Tag
default_category: uncategorized
category_map:
tag_map:

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination
## Set per_page to 0 to disable pagination
per_page: 18
pagination_dir: page

# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: hexo-theme-matery
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy: # 部署
  type: git
  repo: https://github.com/xinetzone/xinetzone.github.io.git
  branch: master

# 自定义
## 添加emoji表情支持
githubEmojis:
  enable: true
  className: github-emoji
  inject: true
  styles:
  customEmojis:

## 代码高亮
prism_plugin:
  mode: 'preprocess'    # realtime/preprocess
  theme: 'tomorrow'
  line_number: true    # default false
  custom_css:

## 内容搜索
search:
  path: search.xml
  field: post

## 添加 RSS 订阅支持
feed:
  type: atom
  path: atom.xml
  limit: 20
  hub:
  content:
  content_limit: 140
  content_limit_delim: ' '
  order_by: -date

## 添加动漫人物 
live2d:  # https://github.com/EYHN/hexo-helper-live2d/blob/master/README.zh-CN.md
  enable: true # 默认 false
  scriptFrom: local # 默认
  pluginRootPath: live2dw/ # 插件在站点上的根目录(相对路径)
  pluginJsPath: lib/ # 脚本文件相对与插件根目录路径
  pluginModelPath: assets/ # 模型文件相对与插件根目录路径
  # scriptFrom: jsdelivr # jsdelivr CDN
  # scriptFrom: unpkg # unpkg CDN
  # scriptFrom: https://cdn.jsdelivr.net/npm/live2d-widget@3.x/lib/L2Dwidget.min.js # 你的自定义 url
  tagMode: false # 标签模式, 是否仅替换 live2d tag标签而非插入到所有页面中
  debug: false # 调试, 是否在控制台输出日志
  # log: false
  model: # https://github.com/xiazeyu/live2d-widget-models
    use: live2d-widget-model-shizuku # npm-module package name，
    # use: wanko # 博客根目录/live2d_models/ 下的目录名
    # use: ./wives/wanko # 相对于博客根目录的路径
    # use: https://cdn.jsdelivr.net/npm/live2d-widget-model-wanko@1.0.5/assets/wanko.model.json # 你的自定义 url
  display:
    position: left
    width: 150
    height: 300
  mobile: # 是否在移动设备上显示
    show: true # 默认 false
    scale: 0.5 # 移动设备上的缩放  
  react:
    opacity: 0.7
```

接着，使用 `npm install` 安装必备包：

```sh
$ npm install
```

关于 `fsevents` 的警告不要管，在 Windows 系统中总会有。但需要升级 `core-js@3`（即 Hexo 3）：

```sh
$ npm install core-js@3
```

更多的配置请 :book: [hexo-theme-matery/README_CN.md](https://github.com/blinkfox/hexo-theme-matery/blob/develop/README_CN.md)。为了可以将 hexo 主题部署到 github，需要：

```sh
$ npm i hexo-deployer-git
$ hexo clean && hexo g
$ hexo d
```

## 修改网站的内容与插件

以下内容参考：<https://godweiyang.com/2018/04/13/hexo-blog/>

### 添加 404 页面

首先在 `/docs/source/` 目录下新建一个 `404.md`，内容如下：

```
---
title: 404
date: 2019-09-02 13:13:10
type: "404"
layout: "404"
description: "你来到了没有知识的荒原 :("
---
```

然后在 `/docs/themes/matery/layout/` 目录下新建一个 `404.ejs` 文件，内容如下：

```js
<style type="text/css">
    /* don't remove. */
    .about-cover {
        height: 75vh;
    }
</style>

<div class="bg-cover pd-header about-cover">
    <div class="container">
        <div class="row">
            <div class="col s10 offset-s1 m8 offset-m2 l8 offset-l2">
                <div class="brand">
                    <div class="title center-align">
                        404
                    </div>
                    <div class="description center-align">
                        <%= page.description %>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<script>
    // 每天切换 banner 图.  Switch banner image every day.
    $('.bg-cover').css('background-image', 'url(/medias/banner/' + new Date().getDay() + '.jpg)');
</script>
```

### “关于”页面增加简历（可选）

修改 `/docs/themes/matery/layout/about.ejs`，找到 `<div class="card">` 标签，然后找到它对应的 `</div>` 标签，接在后面新增一个 card，语句如下：

```js
<div class="card">
    <div class="card-content">
        <div class="card-content article-card-content">
            <div class="title center-align" data-aos="zoom-in-up">
                <i class="fa fa-address-book"></i>&nbsp;&nbsp;<%- __('myCV') %>
            </div>
            <div id="articleContent" data-aos="fade-up">
                <%- page.content %>
            </div>
        </div>
    </div>
</div>
```

这样就会多出一张 card，然后可以在 `/docs/source/about/index.md` 下面写上你的简历了，当然这里的位置随你自己设置，你也可以把简历作为第一个 card。

### 添加动漫人物

```sh
$ npm install --save hexo-helper-live2d
$ npm install live2d-widget-model-shizuku
```

在 `/docs/_config.yml` 最后添加：

```yml
live2d:
  enable: true # 默认为 false
  scriptFrom: local
  pluginRootPath: live2dw/
  pluginJsPath: lib/
  pluginModelPath: assets/
  tagMode: false
  log: false
  model:
    use: live2d-widget-model-shizuku
  display:
    position: left
    width: 200
    height: 400
  mobile:
    show: true # 默认 false
  react:
    opacity: 0.7
```

### 图片添加水印

为了防止别人抄袭你文章，可以把所有的图片都加上水印，方法很简单。

首先新建一个 `/docs/watermark.py`，代码如下：

```py
# -*- coding: utf-8 -*-
import sys
import glob
from PIL import Image
from PIL import ImageDraw
from PIL import ImageFont


def watermark(post_name):
    if post_name == 'all':
        post_name = '*'
    dir_name = 'source/_posts/' + post_name + '/*'
    for files in glob.glob(dir_name):
        im = Image.open(files)
        if len(im.getbands()) < 3:
            im = im.convert('RGB')
            print(files)
        font = ImageFont.truetype('STSONG.TTF', max(30, int(im.size[1] / 20)))
        draw = ImageDraw.Draw(im)
        draw.text((im.size[0] / 2, im.size[1] / 2),
                  u'@godweiyang', fill=(0, 0, 0), font=font)
        im.save(files)


if __name__ == '__main__':
    if len(sys.argv) == 2:
        watermark(sys.argv[1])
    else:
        print('[usage] <input>')
```

字体也放根目录下，自己找字体。然后每次写完一篇文章可以运行 `python3 watermark.py  postname` 添加水印，如果第一次运行要给所有文章添加水印，可以运行 `python3 watermark.py all`。

```sh
$ npm install hexo --save
```

### 修复代码块行号不显示的 bug

修改 `/docs/themes/matery/source/css/matery.css` 第 95 行左右的 `pre` 和 `code` 两段改为如下代码：

```css
pre {
    /* padding: 3.3rem !important; */
    padding: 1.5rem 1.5rem 1.5rem 3.3rem !important;
    margin: 1rem 0 !important;
    background: #272822;
    overflow: auto;
    border-radius: 0.35rem;
    tab-size: 4;
}

code {
    padding: 1px 5px;
    font-family: Inconsolata, Monaco, Consolas, 'Courier New', Courier, monospace;
    /* font-size: 0.91rem; */
    color: #e96900;
    background-color: #f8f8f8;
    border-radius: 2px;
}
```

即 注释掉 `code` 的 `font-size: 0.91rem`，修改 `pre` 的 `padding`。然后在 `/docs/_config.yml` 中设置 `prism_plugin.line_number` 为 `true`。

## 上传主题到 GitHub

上面的一系列操作已经配置了一个可以使用的网站了，为了更加便利的使用主题，我们需要将其备份到 GitHub：

```sh
$ cd .. # 切换回主项目的根目录
$ git add .
$ git commit -m "创建一个hexo demo"
$ git push origin hexo
```

最后还需要将 origin/hexo 设置为 Github 默认仓库。

最终的效果展示可以 :book: <https://xinetzone.github.io>。


## 部署到 GitHub 时图片显示问题

一般情况，hexo3 对于图片的显示可能会出现问题，解决方法是卸载 `hexo-render-marked-lazy`。如果还有问题，那么可能是链接出现问题，解决策略是将默认是链接方式改为永久性链接，:book: [永久链接（Permalinks）](https://hexo.io/zh-cn/docs/permalinks.html) 以及 [abbrlink更新2.0.4说明](https://post.zz173.com/detail/hexo-abbrlink-2.0.4.html)。`/docs/_config.yml` 要做两处修改：

```yml
permalink: :lang/:abbrlink.html # :lang/:title/（多语言） 或者 :year/:month/:day/:title/
abbrlink:
  alg: crc32  # 算法：crc16(default) and crc32
  rep: hex    # 进制：dec(default) and hex
permalink_defaults:
```

与

```yml
# Writing
new_post_name: :lang/:title.md # File name of new posts，支持多语言
```

## 修改首页页脚显示

下面是我修改的部分代码：

```js
<footer class="page-footer bg-color">
    <div class="container row center-align">
        <div class="col s12 m8 l8 copy-right">
            本站由&copy;<a href="https://xinetzone.github.io/" target="_blank">xinetzone</a>基于
            <a href="https://blinkfox.github.io/" target="_blank">闪烁之狐</a> 的
            <a href="https://github.com/blinkfox/hexo-theme-matery" target="_blank">hexo-theme-matery</a>主题搭建.
        </div>
        <div class="col s12 m8 l8">
            <% if (theme.wordCount.enable && theme.wordCount.totalCount) { %>
                &nbsp;<i class="fa fa-area-chart"></i>&nbsp;站点总字数:&nbsp;
                <span class="white-color"><%= totalcount(site) %></span>
            <% } %>
            <span id="sitetime"></span>
            <% let socialClass = '' %>
			<% if (theme.busuanziStatistics && theme.busuanziStatistics.enable) { %>
                <% socialClass = 'social-statis' %><br>
                <% if (theme.busuanziStatistics && theme.busuanziStatistics.totalTraffic) { %>
                <span id="busuanzi_container_site_pv">
                    <i class="fa fa-heart-o"></i>
                    本站总访问量 <span id="busuanzi_value_site_pv" class="white-color"></span>
                </span>
                <% } %>
                <% if (theme.busuanziStatistics && theme.busuanziStatistics.totalNumberOfvisitors) { %>
                <span id="busuanzi_container_site_uv">
                    <i class="fa fa-users"></i>
                    次,&nbsp;访客数 <span id="busuanzi_value_site_uv" class="white-color"></span> 人.
                </span>
                <% } %>
            <% } %>
        </div>
        <div class="col s12 m4 l4 social-link <%- socialClass %>"><%- partial('_partial/social-link') %></div>
    </div>
</footer>
...
```

具体的布局方式，可以参考：[materializecss: 网格](http://www.materializecss.cn/grid.html)。

## 修改社交链接

对于 Github 只需要修改其对应文件的 `/docs/../thems/layout/_partial/social-link.ejs` 为：

```js
<% if (theme.socialLink.github) { %>
    <a href="https://github.com/<%= theme.socialLink.github %>" class="tooltipped" target="_blank" data-tooltip="访问我的GitHub" data-position="top" data-delay="50">
        <i class="fa fa-github"></i>
    </a>
<% } %>
```

可以添加领英：

```js
<% if (theme.socialLink.Linkedin) { %>
    <a href="https://www.linkedin.com/in/<%= theme.socialLink.Linkedin %>" class="tooltipped" data-tooltip="领英联系我: <%= theme.socialLink.Linkedin %>" data-position="top" data-delay="50">
        <i class="fa fa-linkedin"></i>
    </a>
<% } %>
```

## 文章头设置

首先为了新建文章方便，建议将 `/docs/scaffolds/post.md` 修改为如下代码：

```
---
title: {{ title }}
date: {{ date }}
top: false # 推荐文章（文章是否置顶）
cover: false # 表示该文章是否需要加入到首页轮播封面中
password:
toc: true
mathjax: false
comments: true
summary: # 文章摘要
tags: # 文章标签，一篇文章可以多个标签
categories: # 文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类
---

---
版权声明：

除非注明，本博文章均为原创，转载请以链接形式标明本文地址。
---
```

这样新建文章后不用你自己补充了，修改信息就行。

## 部署的项目主页添加 `README`

在部署的项目到 Github 上建立自己的博客仓库的时候并没有生成 README 文件，为此，我们需要在 `/docs/source`下手动新建 `README.md`。然后再在这个新建文件中写 `README` 即可。再之后 `hexo g` 会把它复制到 `/docs/public` 文件夹，而不会被解析成 html 文件，发布在博客中。

## 创建新的页面

首先运行如下命令，生成 :book: 页面：

```sh
$ hexo new page board
```

系统会自动给你在 `/docs/source` 文件夹下创建一个 `book` 文件夹，以及 `book` 文件夹中的 `index.md`，这样你访问的 `book` 对应的链接就是 `http://xxx.xxx/book`。

然后在主题配置文件的 `menu` 菜单栏添加一个 `Yourdiy : /yourdiy`，注意冒号后面要有空格，以及前面的空格要和 `menu` 中默认的保持整齐。然后在 `languages` 文件夹中，找到 `zh-CN.yml`，在 `index` 中添加 `yourdiy: '中文意思'` 就可以显示中文了。

比如在 `zh-CN.yml` 中添加：`book: 书籍`，在 `menu` 菜单栏中添加：

```yml
书籍:
    url: /book
    icon: fa-book
```

如果您觉得麻烦，可以直接 fork 我已经配置好的博客模板 [xinetzone-matery](https://github.com/xinetzone/xinetzone.github.io) 并按照 README 进行操作即可。