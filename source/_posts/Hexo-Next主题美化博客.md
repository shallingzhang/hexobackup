---
title: Hexo+Next主题美化博客
date: 2022-08-31 15:05:15
tags:
  - hexo
  - next
  - 主题
categories:
  - linux
---



## 前言

有了前面那篇如何搭建博客的文章介绍指导，我们现在可以很容易的搭建博客了，不过既然是属于自己的博客网站，自然也就想让其更加美观，Hexo 博客支持很多主题风格，官网 https://hexo.io/themes/ 截止目前拥370个不同风格的主题，下面介绍一下Hexo博客的主题美化操作。

Next 主题 https://theme-next.js.org/ 是为 Hexo 打造的一款高品质优雅主题，支持非常多的外部插件和功能选项。我目前使用的是 NexT.Gemini V8.12.3 版本，下面我会介绍关于 Next 8 主题的基本安装配置和界面美化。

<!-- more -->

## 安装

确保你已经安装了Hexo 并成功地创建了一个站点，因为以下文档要求你在站点根目录(blog_folder)下操作。

### 安装 Next 主题

安装 Hexo 主题的2种方式: 

1. 打开终端，切换到 Hexo 站点根目录，通过 npm 安装 Next 主题:

   ```
   $ cd blog_folder
   $ npm install hexo-theme-next
   ```

2. 打开终端，切换到 Hexo 站点根目录，使用 git下载 Next 主题的源代码:

   ```
   $ cd blog_folder
   $ git clone https://github.com/next-theme/hexo-theme-next themes/next
   ```

### 升级 Next 主题

Next 主题的新版本每月发布一次，请在更新主题前阅读发布说明，可以使用以下命令更新Next主题：

1. 通过npm安装最新版本:

   ```
   $ cd hexo-site
   $ npm install hexo-theme-next@latest
   ```

2. 或者更新到最新的主分支:

   ```
   $ cd blog_folder
   $ cd themes/next
   $ git pull origin master
   ```

## 配置

通过修改配置文件可以直接修改主题样式Git

### 配置文件

在安装 Hexo 和 Next 之后，你可能会发现有两个配置文件被 Hexo 使用，它们都被称为 _config.yml:

1. 第一个在站点根目录 blog_folder下，它包含了Hexo的配置。

2. 第二个在主题根目录下(例如：thems/next/_config. yml 或 node_modules/hexo-theme-next/_config.yml)。它由 Next 提供，包含主题的配置。

让我们把第一个文件叫做 Hexo配置文件，把第二个文件叫做 Next 配置文件。

  > 注意：npm方式安装主题，默认配置文件在node_modules/hexo-theme-next/_config.yml，git方式安装主题，默认配置文件在themes/next/_config.yml 

但是，不建议直接修改主题配置文件，因为通过git或npm升级下一个版本主题时，配置文件会被覆盖，那如何解决这个问题呢？

1. 请确保你使用的是 Hexo 5.0或更高版本。
2. 在站点的根目录下创建一个配置文件：_config.next.yml。
3. 将所需的Next主题选项从NexT配置文件复制到此配置文件。

如果是第一次安装 Next，则使用以下命令复制整个NexT配置文件即可:

   ```
     # Installed through npm
     cp node_modules/hexo-theme-next/_config.yml _config.next.yml

     # Installed through 
     cp themes/next/_config.yml _config.next.yml
   ```

以后所有配置只需要更改站点根目录下的_config.yml和 _config.next.yml两个配置文件就可以了，升级Next时也不会受影响。

### Hexo 基本配置

**更改站点根目录下的 _config.yml 文件**

1. 站点基本配置

   ```
    # Hexo Configuration
    ## Docs: https://hexo.io/docs/configuration.html
    ## Source: https://github.com/hexojs/hexo/

    # Site                      # 站点配置
    title: Shalling's Blog      # 网站标题
    subtitle: '新时代农民工'      # 网站副标题
    description: 'Stay hungry,Stay foolish.'    # 网站描述
    keywords:
    author: Shalling Zhang      # 作者昵称
    language: zh-CN             # 显示语言
    timezone: 'Asia/Shanghai'   # 所在时区
   ```

2. 启用 Next 主题

   ```
    # Extensions
    ## Plugins: https://hexo.io/plugins/
    ## Themes: https://hexo.io/themes/
    #theme: landscape   # 禁用默认主题
    theme: next         # 启用next主题
   ```

3. 更改 Hexo 配置文件后，需要重新生成站点文件，新的主题样式才能生效。

   ```
    $ cd ~/blog_folder
    $ hexo clean
    $ hexo generate
    $ hexo server
   ```

Hexo is running at http://localhost:4000/ . Press Ctrl+C to stop.

### Next 基本配置

**更改站点根目录下的 _config.next.yml 文件**

1. 主题风格方案配置

   Next主题自带4种不同的风格方案，取消哪个方案名称前面的#注释，即采用该方案

   ```
   # ---------------------------------------------------------------
   # Scheme Settings   
   # ---------------------------------------------------------------
   
   # Schemes       # 主题方案（Muse、Mist、Pisces、Gemini 共4种，可任选1种）
   #scheme: Muse
   #scheme: Mist
   #scheme: Pisces
   scheme: Gemini  # 采用 Gemini 方案
   ```

2. 开启夜间模式

   夜间模式没有独立切换开关，会跟随系统主题自动切换显示效果

   ```
      # Dark Mode
      darkmode: true  # true开启，false关闭
   ```

3. 自定义网站图标

   在站点根目录下的source目录新建_uploads文件夹用于存放站点图片资源

   ```
   favicon:
     # small: /images/favicon-16x16-next.png
     # medium: /images/favicon-32x32-next.png
     # apple_touch_icon: /images/apple-touch-icon-next.png
     # safari_pinned_tab: /images/logo.svg
     small: /uploads/favicon-16x16-next.png    # 网站图标路径
     medium: /uploads/favicon-32x32-next.png   # 网站图标路径
     apple_touch_icon: /uploads/apple-touch-icon-next.png
     safari_pinned_tab: /uploads/logo.svg
     #android_manifest: /manifest.json
   ```

4. 配置 “知识共享国际许可协议”

   ```
   # Creative Commons 4.0 International License.
   # See: https://creativecommons.org/about/cclicenses/
   creative_commons:
     # Available values: by | by-nc | by-nc-nd | by-nc-sa | by-nd | by-sa | cc-zero
     license: by-nc-sa   # license 值
     # Available values: big | small
     size: small         # 显示大小
     sidebar: true       # 侧边栏是否显示
     post: true          # 文章是否显示
     # You can set a language value if you prefer a translated version of CC license, e.g. deed.zh
     # CC licenses are available in 39 languages, you can find the specific and correct abbreviation you need on https://creativecommons.org
     language: deed.zh   # 中文
   ```

5. 配置网站菜单栏

   新增加菜单项，需要新增加对应的页面，

   首先，取消 about、tags、categories前面的#注释符号

    ```
       menu:
         home: / || fa fa-home                      # 首页
         about: /about/ || fa fa-user               # 关于
         tags: /tags/ || fa fa-tags                 # 标签
         categories: /categories/ || fa fa-th       # 分类
         archives: /archives/ || fa fa-archive      # 归档
         #schedule: /schedule/ || fa fa-calendar
         #sitemap: /sitemap.xml || fa fa-sitemap
         #commonweal: /404/ || fa fa-heartbeat
    ```

   其次，新增about、tags、categories页面

    ```
     $ hexo new page about           # 新增 about 页面
     $ hexo new page tags            # 新增 tags  页面
     $ hexo new page categories      # 新增 categories 页面
    ```

   在站点根目录source/_posts/下会生成tags、categories、about三个文件夹，每个文件夹中都有一个index.md文件，接下来分别修改每个文件内容。

    标签页
   
     ```
     ---
     title: 标签
     date: 2022-08-19 11:06:30
     type: tags
     ---
     ```

    分类页

    ```
     ---
     title: 分类
     date: 2022-08-19 11:06:43
     type: categories
     ---
    ```

    关于页
   
     ```
     ---
     title: 关于
     date: 2022-08-19 11:06:23
     type: about
     ---
     ```

6. 侧边栏位置

   ```
   sidebar:
     # Sidebar Position.
     # position: left     # 页面左侧
     position: right      # 页面右侧
   ```

7. 更改网站默认头像

   ```
   avatar:
     # Replace the default image and set the url here.
     #url: /images/avatar.gif
     url: /uploads/avatar.png  # 头像图片位置
     # If true, the avatar will be displayed in circle.
     rounded: false   # true 头像外边框显示圆形
     # If true, the avatar will be rotated with the cursor.
     rotated: false   # 鼠标悬浮，图片旋转
   ```

8. 配置社交链接图标

   ```
      social:
        GitHub: https://github.com/shallingzhang || fab fa-github
        E-Mail: mailto:2026355878@qq.com || fa fa-envelope
   ```

9. 配置脚标显示：

   Powered by Hexo & Next 信息是否显示

   ```
   # Powered by Hexo & NexT,true or false to display.
     powered: true  # false 不显示
   ```

   备案信息

   ```
   # Beian ICP and gongan information for Chinese users. See: https://beian.miit.gov.cn, http://www.beian.gov.cn
     beian:
       enable: false    # true 开启显示
       icp: 京ICP备 1234567890号-1
       # The digit in the num of gongan beian.
       gongan_id: 1234567890
       # The full num of gongan beian.
       gongan_num: 京公网安备 1234567890号
       # The icon for gongan beian. See: http://www.beian.gov.cn/portal/download
       gongan_icon_url: /uploads/beian.png
   ```

   

## 插件

### hexo-deployer-git

插件说明

```
# 一键部署功能：让你只需一条命令就能将Hexo网站部署到GitHub服务器上。 
```

安装插件

```
$ npm install hexo-deployer-git --save
```

修改配置

```
$ cd ~/blog_folder
$ vim _config.yml   # 在文件尾部添加如下代码

# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git         # 部署类型 git
  repo: https://github.com/shallingzhang/shallingzhang.github.io  # 仓库地址
  branch: main      # 分支名称 mian
  message:          # 自定义提交信息

```

### hexo-generator-searchdb

插件说明

```
# 搜索数据生成插件:能够生成一个搜索索引文件，该文件包含你的文章的所有必要数据，你可以用这些数据为你的博客编写一个本地搜索引擎。
```

安装插件

```
$ npm install hexo-generator-searchdb --save
```

修改配置

```
$ cd ~/blog_folder
$ vim _config.yml       # 在文件尾部添加如下代码

#Search
## Plugins : hexo-generator-searchdb,local search engine.
search:
  path: search.xml
  field: post
  content: true
  format: html

$ vim _config.next.yml  # true，开启本地搜索菜单
local_search:
  enable: true
```

### hexo-word-counter

插件说明

```
# 在 Hexo 博客站点中统计文章的符号个数和阅读时间
```

安装插件

```
$ npm install hexo-word-counter --save
```

修改配置

```
$ cd ~/blog_folder
$ vim _config.yml       # 在文件尾部添加如下代码

# hexo-word-counter
## Plugins : hexo-word-counter,local count engine.
symbols_count_time:
  symbols: true
  time: true
  total_symbols: true
  total_time: true
  exclude_codeblock: false
  awl: 4
  wpm: 275
  suffix: "mins."
```



## 美化

### 看板娘
安装插件
```
$ npm install --save hexo-helper-live2d
```

安装模型

```
$ npm install --save live2d-widget-model-z16
```

配置显示

请向 Hexo 的 _config.yml 文件或主题的 _config.next.yml 文件中添加配置.

```
live2d:
  enable: true
  scriptFrom: local
  pluginRootPath: live2dw/
  pluginJsPath: lib/
  pluginModelPath: assets/
  tagMode: false
  log: false
  model:
    use: live2d-widget-model-z16
  display:
    position: right
    width: 150
    height: 300
  mobile:
    show: true
  react:
    opacity: 0.7
```

可用模型列表

```
live2d-widget-model-chitose
live2d-widget-model-epsilon2_1
live2d-widget-model-gf
live2d-widget-model-haru/01 (use npm install --save live2d-widget-model-haru)
live2d-widget-model-haru/02 (use npm install --save live2d-widget-model-haru)
live2d-widget-model-haruto
live2d-widget-model-hibiki
live2d-widget-model-hijiki
live2d-widget-model-izumi
live2d-widget-model-koharu
live2d-widget-model-miku
live2d-widget-model-ni-j
live2d-widget-model-nico
live2d-widget-model-nietzsche
live2d-widget-model-nipsilon
live2d-widget-model-nito
live2d-widget-model-shizuku
live2d-widget-model-tororo
live2d-widget-model-tsumiki
live2d-widget-model-unitychan
live2d-widget-model-wanko
live2d-widget-model-z16
```

卸载模型

```
$ npm uninstall live2d-widget-model-z16
```

### 页面圆角与顶部边距

在站点根目录下的source文件夹中创建_data文件夹，用于存放自定义页面内容

```
$ mkdir ~/blog_folder/source/_data
$ cd ~/blog_folder/source/_data
$ touch variables.styl 
$ touch styles.styl 
```

配置 /source/_data/variables.styl ，默认没有，需要新建 variables.styl 

```
// 页面圆角设置
$border-radius-inner     = 18px 18px 18px 18px;
$border-radius           = 18px;
```

配置 /source/_data/styles.styl ，默认没有，需要新建 styles.styl 

```
/* 顶部边距 */
.header,
.main-inner {
  margin-top: 10px;

  +mobile() {
    margin-top: 0;
  }
}

/* 侧边栏圆角 */

.site-brand-container {
  border-radius: 18px 18px 0 0;

  +mobile() {
    border-radius: 0 0 0 0;
  }
}
```

修改主题配置文件 _config.next.yml，开启自定义页面相关配置

```
custom_file_path:
  #head: source/_data/head.njk
  #header: source/_data/header.njk
  #sidebar: source/_data/sidebar.njk   
  #postMeta: source/_data/post-meta.njk
  #postBodyEnd: source/_data/post-body-end.njk
  #footer: source/_data/footer.njk
  #bodyEnd: source/_data/body-end.njk
  variable: source/_data/variables.styl  # 取消该行的注释
  #mixin: source/_data/mixins.styl
  style: source/_data/styles.     # 取消该行的注释
```



### 背景图片

自定义背景图片，需要现将自己喜欢的图片（建议大小 200K 以内）放在 source/uploads目录下，并重命名为 background

然后配置 source/_data/ styles.styl 

```
// 添加背景图片
body {
      background: url(/uploads/background.jpg); //自己喜欢的图片地址
      background-size: cover;
      background-repeat: no-repeat;
      background-attachment: fixed;
      background-position: 50% 50%;
      @media (prefers-color-scheme: dark) {
        background-image: none;
      }
}
```

### 页面透明度

配置 source/_data/ styles.styl 

```
//博客内容透明化 0-1
//文章内容的透明度设置
.main-inner {
  opacity: 0.8;
}

//侧边框的透明度设置
.sidebar {
  opacity: 0.8;
}

// 菜单栏的透明度设置

.header-inner {
  background: rgba(255,255,255,0.8);
  @media (prefers-color-scheme: dark) {
     background: rgba(51,51,51,0.8);
  }
}

//搜索框（local-search）的透明度设置
.popup {
  opacity: 0.9;
}
```

### 页面加载进度条

修改主题配置文件 _config.next.yml 

```
# Progress bar in the top during page loading.
# For more information: https://github.com/CodeByZach/pace
pace:
  enable: true    # 开启显示
  # All available colors:
  # black | blue | green | orange | pink | purple | red | silver | white | yellow
  color: blue     # 样式
  # All available themes:
  # big-counter | bounce | barber-shop | center-atom | center-circle | center-radar | center-simple
  # corner-indicator | fill-left | flat-top | flash | loading-bar | mac-osx | material | minimal
  theme: minimal  # 颜色
```

### 背景动画：随机丝带

修改主题配置文件 _config.next.yml 

```
# Canvas ribbon
# For more information: https://github.com/hustcc/ribbon.js
canvas_ribbon:
  enable: true  # 开启显示
  size: 300 # The width of the ribbon
  alpha: 0.6 # The transparency of the ribbon
  zIndex: -1 # The display level of the ribbon
```

### 站点访问统计

修改主题配置文件 _config.next.yml 

```
# Show Views / Visitors of the website / page with busuanzi.
# For more information: http://ibruce.info/2015/04/04/busuanzi/
busuanzi_count:
  enable: true
  total_visitors: true
  total_visitors_icon: fa fa-user
  total_views: true
  total_views_icon: fa fa-eye
  post_views: true
  post_views_icon: far fa-eye
```

### 字体

修改主题配置文件 _config.next.yml 

```
# ---------------------------------------------------------------
# Font Settings
# ---------------------------------------------------------------
# Find fonts on Google Fonts (https://fonts.google.com)
# All fonts set here will have the following styles:
#   light | light italic | normal | normal italic | bold | bold italic
# Be aware that setting too much fonts will cause site running slowly
# ---------------------------------------------------------------
# Web Safe fonts are recommended for `global` (and `title`):
# Arial | Tahoma | Helvetica | Times New Roman | Courier New | Verdana | Georgia | Palatino | Garamond | Comic San
 MS | Trebuchet MS
# ---------------------------------------------------------------

font:
  enable: true

  # Uri of fonts host, e.g. https://fonts.googleapis.com (Default).
  host:  
 
  # Font options:
  # `external: true` will load this font family from `host` above.
  # `family: Times New Roman`. Without any quotes.
  # `size: x.x`. Use `em` as unit. Default: 1 (16px)

  # Global font settings used for all elements inside <body>.
  global:
    external: true
    family: Lato
    size:

  # Font settings for site title (.site-title).
  title:
    external: true
    family:
    size:

  # Font settings for headlines (<h1> to <h6>).
  headings:
    external: true
    family:
    size:

  # Font settings for posts (.post-body).
  posts:
    external: true
    family:

  # Font settings for <code> and code blocks.
  codes:
    external: true
    family:
```

### 鼠标

安装fireworks点击特效动画

```
npm install next-theme/hexo-next-fireworks  # Fireworks animation for NexT.
```

### 代码块

修改主题配置文件 _config.next.yml 

```
codeblock:
  # Code Highlight theme
  # All available themes: https://theme-next.js.org/highlight/
  theme:  # 代码块主题配色
    #light: default
    #dark: stackoverflow-dark
    light: base16/tomorrow-night
    dark: base16/tomorrow-night
  prism:
    light: prism
    dark: prism-dark
  # Add copy button on codeblock
  copy_button:
    enable: true   # 启用复制按钮
    # Available values: default | flat | mac
    style: default
```

### 粒子钟

修改主题配置文件 _config.next.yml 

```
custom_file_path:
  # head: source/_data/head.njk
  #header: source/_data/header.njk
  sidebar: source/_data/sidebar.njk   ## 取消该行的注释；这个针对侧边栏的样式自定义
  #postMeta: source/_data/post-meta.njk
  postBodyEnd: source/_data/post-body-end.njk
  footer: source/_data/footer.njk
  bodyEnd: source/_data/body-end.njk
  variable: source/_data/variables.styl
  #mixin: source/_data/mixins.styl
  style: source/_data/styles.styl
```

新建侧边栏粒子钟配置文件 source/_data/sidebar.njk，添加如下代码：

```
<div style="">
  <canvas id="canvas" style="width:60%;">当前浏览器不支持canvas，请更换浏览器后再试</canvas>
</div>
<script>
(function(){

   var digit=
    [
        [
            [0,0,1,1,1,0,0],
            [0,1,1,0,1,1,0],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [0,1,1,0,1,1,0],
            [0,0,1,1,1,0,0]
        ],//0
        [
            [0,0,0,1,1,0,0],
            [0,1,1,1,1,0,0],
            [0,0,0,1,1,0,0],
            [0,0,0,1,1,0,0],
            [0,0,0,1,1,0,0],
            [0,0,0,1,1,0,0],
            [0,0,0,1,1,0,0],
            [0,0,0,1,1,0,0],
            [0,0,0,1,1,0,0],
            [1,1,1,1,1,1,1]
        ],//1
        [
            [0,1,1,1,1,1,0],
            [1,1,0,0,0,1,1],
            [0,0,0,0,0,1,1],
            [0,0,0,0,1,1,0],
            [0,0,0,1,1,0,0],
            [0,0,1,1,0,0,0],
            [0,1,1,0,0,0,0],
            [1,1,0,0,0,0,0],
            [1,1,0,0,0,1,1],
            [1,1,1,1,1,1,1]
        ],//2
        [
            [1,1,1,1,1,1,1],
            [0,0,0,0,0,1,1],
            [0,0,0,0,1,1,0],
            [0,0,0,1,1,0,0],
            [0,0,1,1,1,0,0],
            [0,0,0,0,1,1,0],
            [0,0,0,0,0,1,1],
            [0,0,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [0,1,1,1,1,1,0]
        ],//3
        [
            [0,0,0,0,1,1,0],
            [0,0,0,1,1,1,0],
            [0,0,1,1,1,1,0],
            [0,1,1,0,1,1,0],
            [1,1,0,0,1,1,0],
            [1,1,1,1,1,1,1],
            [0,0,0,0,1,1,0],
            [0,0,0,0,1,1,0],
            [0,0,0,0,1,1,0],
            [0,0,0,1,1,1,1]
        ],//4
        [
            [1,1,1,1,1,1,1],
            [1,1,0,0,0,0,0],
            [1,1,0,0,0,0,0],
            [1,1,1,1,1,1,0],
            [0,0,0,0,0,1,1],
            [0,0,0,0,0,1,1],
            [0,0,0,0,0,1,1],
            [0,0,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [0,1,1,1,1,1,0]
        ],//5
        [
            [0,0,0,0,1,1,0],
            [0,0,1,1,0,0,0],
            [0,1,1,0,0,0,0],
            [1,1,0,0,0,0,0],
            [1,1,0,1,1,1,0],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [0,1,1,1,1,1,0]
        ],//6
        [
            [1,1,1,1,1,1,1],
            [1,1,0,0,0,1,1],
            [0,0,0,0,1,1,0],
            [0,0,0,0,1,1,0],
            [0,0,0,1,1,0,0],
            [0,0,0,1,1,0,0],
            [0,0,1,1,0,0,0],
            [0,0,1,1,0,0,0],
            [0,0,1,1,0,0,0],
            [0,0,1,1,0,0,0]
        ],//7
        [
            [0,1,1,1,1,1,0],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [0,1,1,1,1,1,0],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [0,1,1,1,1,1,0]
        ],//8
        [
            [0,1,1,1,1,1,0],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [1,1,0,0,0,1,1],
            [0,1,1,1,0,1,1],
            [0,0,0,0,0,1,1],
            [0,0,0,0,0,1,1],
            [0,0,0,0,1,1,0],
            [0,0,0,1,1,0,0],
            [0,1,1,0,0,0,0]
        ],//9
        [
            [0,0,0,0,0,0,0],
            [0,0,1,1,1,0,0],
            [0,0,1,1,1,0,0],
            [0,0,1,1,1,0,0],
            [0,0,0,0,0,0,0],
            [0,0,0,0,0,0,0],
            [0,0,1,1,1,0,0],
            [0,0,1,1,1,0,0],
            [0,0,1,1,1,0,0],
            [0,0,0,0,0,0,0]
        ]//:
    ];

var canvas = document.getElementById('canvas');

if(canvas.getContext){
    var cxt = canvas.getContext('2d');
    //声明canvas的宽高
    var H = 100,W = 700;
    canvas.height = H;
    canvas.width = W;
    cxt.fillStyle = '#f00';
    cxt.fillRect(10,10,50,50);

    //存储时间数据
    var data = [];
    //存储运动的小球
    var balls = [];
    //设置粒子半径
    var R = canvas.height/20-1;
    (function(){
        var temp = /(\d)(\d):(\d)(\d):(\d)(\d)/.exec(new Date());
        //存储时间数字，由十位小时、个位小时、冒号、十位分钟、个位分钟、冒号、十位秒钟、个位秒钟这7个数字组成
        data.push(temp[1],temp[2],10,temp[3],temp[4],10,temp[5],temp[6]);
    })();

    /*生成点阵数字*/
    function renderDigit(index,num){
        for(var i = 0; i < digit[num].length; i++){
            for(var j = 0; j < digit[num][i].length; j++){
                if(digit[num][i][j] == 1){
                    cxt.beginPath();
                    cxt.arc(14*(R+2)*index + j*2*(R+1)+(R+1),i*2*(R+1)+(R+1),R,0,2*Math.PI);
                    cxt.closePath();
                    cxt.fill();
                }
            }
        }
    }

    /*更新时钟*/
    function updateDigitTime(){
        var changeNumArray = [];
        var temp = /(\d)(\d):(\d)(\d):(\d)(\d)/.exec(new Date());
        var NewData = [];
        NewData.push(temp[1],temp[2],10,temp[3],temp[4],10,temp[5],temp[6]);
        for(var i = data.length-1; i >=0 ; i--){
            //时间发生变化
            if(NewData[i] !== data[i]){
                //将变化的数字值和在data数组中的索引存储在changeNumArray数组中
                changeNumArray.push(i+'_'+(Number(data[i])+1)%10);
            }
        }
        //增加小球
        for(var i = 0; i< changeNumArray.length; i++){
            addBalls.apply(this,changeNumArray[i].split('_'));
        }
        data = NewData.concat();
    }

    /*更新小球状态*/
    function updateBalls(){
        for(var i = 0; i < balls.length; i++){
            balls[i].stepY += balls[i].disY;
            balls[i].x += balls[i].stepX;
            balls[i].y += balls[i].stepY;
            if(balls[i].x > W + R || balls[i].y > H + R){
                balls.splice(i,1);
                i--;
            }
        }
    }

    /*增加要运动的小球*/
    function addBalls(index,num){
        var numArray = [1,2,3];
        var colorArray =  ["#3BE","#09C","#A6C","#93C","#9C0","#690","#FB3","#F80","#F44","#C00"];
        for(var i = 0; i < digit[num].length; i++){
            for(var j = 0; j < digit[num][i].length; j++){
                if(digit[num][i][j] == 1){
                    var ball = {
                        x:14*(R+2)*index + j*2*(R+1)+(R+1),
                        y:i*2*(R+1)+(R+1),
                        stepX:Math.floor(Math.random() * 4 -2),
                        stepY:-2*numArray[Math.floor(Math.random()*numArray.length)],
                        color:colorArray[Math.floor(Math.random()*colorArray.length)],
                        disY:1
                    };
                    balls.push(ball);
                }
            }
        }
    }

    /*渲染*/
    function render(){
        //重置画布宽度，达到清空画布的效果
        canvas.height = 100;
        //渲染时钟
        for(var i = 0; i < data.length; i++){
            renderDigit(i,data[i]);
        }
        //渲染小球
        for(var i = 0; i < balls.length; i++){
            cxt.beginPath();
            cxt.arc(balls[i].x,balls[i].y,R,0,2*Math.PI);
            cxt.fillStyle = balls[i].color;
            cxt.closePath();
            cxt.fill();
        }
    }

    clearInterval(oTimer);
    var oTimer = setInterval(function(){
        //更新时钟
        updateDigitTime();
        //更新小球状态
        updateBalls();
        //渲染
        render();
    },50);
}

})();
</script>

<div class="site-overview-wrap sidebar-panel{% if not display_toc or toc(page.content).length <= 1 %} sidebar-panel-active{% endif %}">
<div class="site-overview">
    

{% if theme.recent_posts %}
    <div class="links-of-blogroll motion-element {{ "links-of-blogroll-" + theme.recent_posts_layout  }}">
    <div class="links-of-blogroll-title">
        <!-- modify icon to fire by szw -->
        <i class="fa fa-history fa-{{ theme.recent_posts_icon | lower }}" aria-hidden="true"></i>
        {{ theme.recent_posts_title }}
    </div>
    <ul class="links-of-blogroll-list">
        {% set posts = site.posts.sort('-date') %}
        {% for post in posts.slice('0', '5') %}
        <li>
            <a href="{{ url_for(post.path) }}" title="{{ post.title }}" target="_blank">{{ post.title }}</a>
        </li>
        {% endfor %}
    </ul>
    </div>
{% endif %}
</div>
</div>

```

编辑 source/_data/styles.styl 样式文件，添加如下代码：

```
// 粒子时钟样式
.site-overview {
  text-align: center;
}

canvas#canvas {
  margin-top: 20px;
}

```

### 雪花飞舞

新建  blog_folder/node_modules/hexo-theme-next/source/js/snow.js文件，添加如下代码：

```
/* 雪花飞舞 */
(function ($) {
    $.fn.snow = function (options) {
        var $flake = $('<div id="snowbox" />').css({
                'position': 'absolute',
                'z-index': '9999',
                'top': '-50px'
            }).html('❄'),
            documentHeight = $(document).height(),
            documentWidth = $(document).width(),
            defaults = {
                minSize: 10,
                maxSize: 20,
                newOn: 1000,
                flakeColor: "#AFDAEF" /* 此处可以定义雪花颜色，若要白色可以改为#FFFFFF */
            },
            options = $.extend({}, defaults, options);
        var interval = setInterval(function () {
            var startPositionLeft = Math.random() * documentWidth - 100,
                startOpacity = 0.6 + Math.random(),
                sizeFlake = options.minSize + Math.random() * options.maxSize,
                endPositionTop = documentHeight - 200,
                endPositionLeft = startPositionLeft - 500 + Math.random() * 500,
                durationFall = documentHeight * 10 + Math.random() * 5000;
            $flake.clone().appendTo('body').css({
                left: startPositionLeft,
                opacity: startOpacity,
                'font-size': sizeFlake,
                color: options.flakeColor
            }).animate({
                top: endPositionTop,
                left: endPositionLeft,
                opacity: 0.3
            }, durationFall, 'linear', function () {
                $(this).remove()
            });
        }, options.newOn);
    };
})(jQuery);
$(function () {
    $.fn.snow({
        minSize: 5,
        /* 定义雪花最小尺寸 */
        maxSize: 50,
        /* 定义雪花最大尺寸 */
        newOn: 300 /* 定义密集程度，数字越小越密集 */
    });
});

```

新建 source/_data/body-end.styl 样式文件，添加如下代码：

```
<!-- 引入jQuery -->
<script type="text/javascript" src="//libs.baidu.com/jquery/1.8.3/jquery.min.js"></script>

<!-- 雪花特效 -->
<script type="text/javascript" src="/js/snow.js"></script>

```

修改主题配置文件 _config.next.yml，开启自定义页面相关配置

```
custom_file_path:
  #head: source/_data/head.njk
  #header: source/_data/header.njk
  #sidebar: source/_data/sidebar.njk   
  #postMeta: source/_data/post-meta.njk
  #postBodyEnd: source/_data/post-body-end.njk
  #footer: source/_data/footer.njk
  bodyEnd: source/_data/body-end.njk   # 取消该行的注释
  #variable: source/_data/variables.styl  
  #mixin: source/_data/mixins.styl
  #style: source/_data/styles.     
```



## 参考站点

https://vkali.com/categories/Hexo/

http://yearito.cn/categories/

https://pinlyu.com/

https://github.com/next-theme/awesome-next

https://zerobio.github.io/archives/c9759728.html
