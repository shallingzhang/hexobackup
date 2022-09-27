---
title: Hexo博客的备份与恢复
date: 2022-09-27 13:23:47
tags:
  - github
  - 备份
categories:
  - hexo
---

##  备份
### 背景

Hexo 博客源文件是保留在本地的，hexo deploy 部署的文件只是 hexo 生成的静态网页文件，由于本人是在 Linux 虚拟机环境下搭建 Hexo 博客开发环境的，而虚拟机经常重做系统，一旦忘记备份 Hexo 博客源文件，就会导致以前的博客无法更新维护了。

###  思路

在 Github 上新建一个仓库 hexobackup，专门用于备份保存hexo 博客源代码

这样备份博客源文件的好处：

- 如果电脑突然罢工，我们的源文件也不会丢失。
- 在重做系统或更换电脑的时候，我们直接 clone 备份仓库到本地就可以了。

### 操作

<!--more-->

#### 前提准备

- 你已经初始化好了自己想要备份的那个博客。
- 操作系统上 GIT、GitHub 的环境也已经准备好了。

由于 hexo deploy上传部署到 git hub pages 的其实是 hexo 编译后的文件，在本地目录里自动生成的 .deploy_git里面，是用来生成网页的，不包含源文件。而其它文件 ，包括我们写在 source 里面的文章、配置文件、主题文件，都没有上传到 git hub 仓库。

#### 详细步骤

1. 在 github上建一个仓库，命令为 hexobackup ,(这里名称自己随便起)。

2. 原始的博客根目录 blog_folder 下只有 .deploy_git （隐藏文件夹），是没有.git文件夹的，于是我们先去自己的家目录或者桌面等随便一个地方，把刚刚的 hexobackup 仓库给 clone下来。然后剪切出里面的 .git 隐藏文件夹，复制到需要备份的博客根目录 blog_folder下。

```
   git clone git@gitee.com:shallingzhang/hexobackup.git
   // git@gitee.com:shallingzhang/hexobackup.git 改为你自己的备份仓库
```

3. 在博客根目录下修改 .gitignore 配置文件，用来在上传时候忽略一些文件，即不上传 .gitignore 配置文件中忽略的文件。此文件有就直接修改，没有的话请自己手动添加。
.gitignore 配置文件内容如下：

```
   .DS_Store
   Thumbs.db
   db.json
   *.log
   node_modules/
   public/
   .deploy*/
   _multiconfig.yml
```

   > 注意，如果你之前克隆过theme中的主题文件，那么应该把主题文件中的.git文件夹删掉，因为git不能嵌套上传，最好是显示隐藏文件，检查一下有没有，否则上传的时候会出错，导致你的主题文件无法上传，这样你的配置在别的电脑上就用不了。

   hexo 的源文件作用说明：

```
   _config.yml  站点的配置文件，需要拷贝；
   themes/  主题文件夹，需要拷贝；
   source/  博客文章的.md文件，需要拷贝；
   scaffolds/  文章的模板，需要拷贝；
   package.json  安装包的名称，需要拷贝；
   .gitignore  限定在push时哪些文件可以忽略，需要拷贝；
   .git/  主题和站点都有，标志这是一个git项目，不需要拷贝；
   node_modules/  是安装包的目录，在执行npm install的时候会重新生成，不需要拷贝；
   public/  是hexo g生成的静态网页，不需要拷贝；
   .deploy_git  同上，hexo g也会生成，不需要拷贝；
   db.json  自动生成文件，不需要拷贝。
   
   # 其实不需要拷贝的文件正是.gitignore中所忽略的。
```

4. 通过在hexo博客的根目录下执行如下命令，将本地文件备份到 Github 上。

```
   git add .
   git commit  -m  "backup20220819"  （注：“backup20220819”是 git 提交变更标注信息，你可以自定义）
   git push -u origin main   （注：此操作目的是把本地仓库push到github上面hexobackup仓库的main分支）
```

## 恢复

### 前提准备

Hexo 基础开发环境已经部署好，包括 nodejs (已集成npm) ,git等。

### 详细步骤

1. 克隆备份仓库到本地

```
git clone https://gitee.com/shallingzhang/hexobackup.git
// https://gitee.com/shallingzhang/hexobackup.git 换成你自己的仓库
```

2. 安装所需程序及插件

在博客根目录下执行如下命令，在此不需要执行hexo init这条指令，因为不是从零搭建起新博客。

```
npm install hexo-cli -g
npm install hexo-deployer-git
```

3. 重新生成网站文件

```
hexo clean
hexo generate
hexo server
```

4. 访问本地站点 http://localhost:4000 查看是否恢复成功。
