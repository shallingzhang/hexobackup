---
title: 关于hexo-helper-live2d与busuanzi-count冲突
date: 2022-09-07 11:27:21
tags:
  - next
  - live2d
  - busuanzi
categories: 
  - hexo
---

##  前言

在我安装了 `hexo-helper-live2d` 插件配置了网页宠物之后，发现 `busuanzi` 统计功能失效了，那我们有必要重新将它开启。

## 问题

我的 `Next` 主题的 `version` 是 `8.10.1`；`Next` 主题关于 `live2d` 和 `busuanzi` 的不兼容性，官方也在 `Github issue` 上进行了讨论，但是也没有很好的解决办法。有兴趣的同学可以自行前往 `Github issue` 查看。

`Github issue:` https://github.com/EYHN/hexo-helper-live2d/issues/161

`https://boyinthesun.cn/post/error-live2d-busuanzi/` 我根据 `Github issue` 提供的解决办法，针对于 `Next-8.10.1` 失败，并没有解决我的问题，于是在 `https://boyinthesun.cn/post/error-live2d-busuanzi/` 基础上，终于通过下面的办法实现了这两个插件的共存。

通过查看网页源码，发现在 `busuanzi` 插入的 `<span>` 标签中多了个 `style`。

[![img](https://zerobio.github.io/images/image-20220312231832625.png)](https://zerobio.github.io/images/image-20220312231832625.png)

`style="display: none;"` 这个样式存在代表着这个区块将不会才页面中显示；而当我们将 `none` 修改成 `inline` 之后，会发现当前页面中的 `阅读次数：` 出现了，于是我们找到了问题所在。

<!--more-->

## 解决

同 `https://boyinthesun.cn/post/error-live2d-busuanzi/` 帖子提到的办法，先将 `busuanzi.pure.mini.js` 下载到本地，并存放至 `<hexo-site>/node_modules/hexo-theme-next/source/js/` ；接着我们找到 `Next` 主题关于 `busuanzi` 的设置。对于新手来说，很难找到这个 `.njk`。于是我们可以在站点根目录下通过 `find` 命令来查找关键字。

```
cd <hexo-site>
find ./ -name "busuanzi*"
## 输出结果
## ./node_modules/hexo-theme-next/layout/_third-party/statistics/busuanzi-counter.njk
```

于是我们找到了 `./node_modules/hexo-theme-next/layout/_third-party/statistics/busuanzi-counter.njk` 发现里面是这样的。

```
{%- if theme.busuanzi_count.enable %}
  <script{{ pjax }} async src="https://busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
{%- endif %}
```

这里是通过 `url` 插入 `busuanzi` 的，但是我们需要对这个 `js` 文件进行修改，于是我们需要将这个文件下载到本地

将 `https://busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js` 下载至 `<hexo-site>/node_modules/hexo-theme-next/source/js/`，并将 `./node_modules/hexo-theme-next/layout/_third-party/statistics/busuanzi-counter.njk` 修改至下：

```
{%- if theme.busuanzi_count.enable %}
  <script{{ pjax }} async src="/js/busuanzi.pure.mini.js"></script>
{%- endif %}
```

对 `<hexo-site>/source/js/busuanzi.pure.mini.js` 修改如下：

```
var bszCaller,bszTag;!function(){var c,d,e,a=!1,b=[];ready=function(c){return a||"interactive"===document.readyState||"complete"===document.readyState?c.call(document):b.push(function(){return c.call(this)}),this},d=function(){for(var a=0,c=b.length;c>a;a++)b[a].apply(document);b=[]},e=function(){a||(a=!0,d.call(window),document.removeEventListener?document.removeEventListener("DOMContentLoaded",e,!1):document.attachEvent&&(document.detachEvent("onreadystatechange",e),window==window.top&&(clearInterval(c),c=null)))},document.addEventListener?document.addEventListener("DOMContentLoaded",e,!1):document.attachEvent&&(document.attachEvent("onreadystatechange",function(){/loaded|complete/.test(document.readyState)&&e()}),window==window.top&&(c=setInterval(function(){try{a||document.documentElement.doScroll("left")}catch(b){return}e()},5)))}(),bszCaller={fetch:function(a,b){var c="BusuanziCallback_"+Math.floor(1099511627776*Math.random());window[c]=this.evalCall(b),a=a.replace("=BusuanziCallback","="+c),scriptTag=document.createElement("SCRIPT"),scriptTag.type="text/javascript",scriptTag.defer=!0,scriptTag.src=a,scriptTag.referrerPolicy="no-referrer-when-downgrade",document.getElementsByTagName("HEAD")[0].appendChild(scriptTag)},evalCall:function(a){return function(b){ready(function(){try{a(b),scriptTag.parentElement.removeChild(scriptTag)}catch(c){bszTag.hides()}})}}},bszCaller.fetch("//busuanzi.ibruce.info/busuanzi?jsonpCallback=BusuanziCallback",function(a){bszTag.texts(a),bszTag.shows()}),bszTag={bszs:["site_pv","page_pv","site_uv"],texts:function(a){this.bszs.map(function(b){var c=document.getElementById("busuanzi_value_"+b);c&&(c.innerHTML=a[b])})},hides:function(){this.bszs.map(function(a){var b=document.getElementById("busuanzi_container_"+a);b&&(b.style.display="inline")})},shows:function(){this.bszs.map(function(a){var b=document.getElementById("busuanzi_container_"+a);b&&(b.style.display="inline")})}};
```

你可以直接复制粘贴覆盖之前的 `busuanzi.pure.mini.js`，或者找到 `b.style.display="none"` 修改为 `b.style.display="inline"`

最后直接 `hexo clean && hexo s` 重启服务即可。

## 参考链接

[1] https://boyinthesun.cn/post/error-live2d-busuanzi/

## 转载声明

免责声明：
    本文转自网络文章，转载此文章仅为个人收藏，分享知识，如有侵权，请联系博主进行删除。

原文作者：zerobio 

原文地址：https://zerobio.github.io/archives/c9759728.html

