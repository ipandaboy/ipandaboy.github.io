---
title: 在Mac上使用Hexo搭建个人博客
date: 2021-10-17 14:25:56
categories: 其他
tags: [博客]
---

# 安装Hexo

## [Hexo](https://hexo.io)简介

#### 快速、简洁且高效的博客框架，详情查看官网



## Hexo搭建

#### 安装Node.js

下载[Node.js](https://nodejs.org/en/download/) 一路安装好Node.js跟npm

#### 安装Hexo

 ```shell
 sudo npm install -g hexo-cli
 ```

执行以下命令，可直接运行hexo

```shell
echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile
```

创建blog文件夹并在里面初始化Hexo

```shell
mkdir blog 
cd blog
hexo init
```

可以看到blog里面有好几个文件夹

介绍一下每个文件跟文件夹的功能

* _config.yml
  网站的配置文件，可以在此配置大部分参数

* source
  资源文件夹是存放用户资源的地方。除 posts 文件夹之外，开头命名为 (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去。

* themes
  主题文件夹，后面我们使用的next主题即会存放在此。
* landscape

* _posts
  存储你发表在博客上的文章，当Hexo 初始化一个站点时，里面会有一篇默认的博文
* Hello-world.md
* node_modules
* package.json
* scaffolds

* 

执行

```shell
hexo g & hexo s
```

浏览器打开 http://localhost:4000 就可以看到Hello World

一些常见命令

```shell
hexo n page "test"
hexo clean
hexo g
hexo s
```

初步hexo已经安装完毕



## Github 建站

1.在github上创建一个项目，项目名称<#你的id#>.github.io我的id是ipandaboy所以是ipandaboy.github.io

习惯使用master为默认主分支，修改main为master(后面要用到)

添加README.md，随便写点什么都行

先将项目clone下来，我用的是Github Desktop客户端clone下来的

新建hexo分支，用来存放源代码，master分支用于hexo博客显示，把blog文件夹所有东西复制到ipandaboy.github.io文件夹

添加忽略文件

```shell
touch .gitignore
vim .gitignore
```

输入以下内容

```
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
themes/
```



#### 配置SSH Keys

* 输入设置命令

```shell
git config --global user.name "yourname"
git config --global user.email "youremail"
```

* 验证是否输对

```shell
git config user.name
git config user.email
```

* 创建SSH

```shell
ssh-keygen -t rsa -C "youremail"
```

* 查看内容

```shell
cd ~/.ssh
ls
cat id_rsa.pub
```

有私钥id_rsa和公钥id_rsa.pub两个文件,把cat出来的内容复制，粘贴到github上

![](/images/hexo_new_ssh.png)

#### 安装 hexo-deployer-git

安装部署命令工具deploy-git 才能用命令部署到GitHub

```shell
npm install hexo-deployer-git --save
```

修改_config.yml文件,这边的branch是master，hexo是源代码，master是博客html

```
deploy:
  type: git
  repo: https://github.com/ipandaboy/ipandaboy.github.io.git
  branch: master
```

部署命令

```shell
hexo clean
hexo generate
hexo deploy
```

执行成功后打开https://ipandaboy.github.io 就可以看到Hellworld网站了

github上ipandaboy.github.io项目的master分支也有了网站代码。而hexo分支是源代码，注意：不要把两个分支合并



5.搭建域名（没有的跳过）

!!!!

!!!!

!!!!



# 其他建站

目前暂时不考虑其他平台搭建，后续有需要再补上

@@@

@@@

@@@



# 优化Hexo

### 修改_config.yml默认设置

```
# Site
title: iPandaBoy
subtitle: ''
description: '做一条最闲的咸鱼'
keywords:
author: iPandaBoy
language: zh-CN
timezone: ''

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://ipandaboy.github.io
root: /
```



### Next主题

Hexo上有很多主题，比较喜欢Next

```shell
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

修改_config.yml

* theme: next

### 主题个性设置

官方设置 https://theme-next.iissnan.com

1.修改样式

 ```
 # Schemes
 # scheme: Muse
 #scheme: Mist
 #scheme: Pisces
 scheme: Gemini
 ```

2.设置菜单

```
home: / || fa fa-home
about: /about/ || fa fa-user
tags: /tags/ || fa fa-tags
categories: /categories/ || fa fa-th
archives: /archives/ || fa fa-archive
```

需要添加about页

```
hexo new page "about"
```

修改文件代码 source/tags/index.md ，自己随便写点什么吧



需要添加tags页

```
hexo new page "tags"
```

修改文件代码 source/tags/index.md

```
title: 标签
date: 2021-10-15 15:09:46
type: tags
layout: tags
```



需要添加categories

```
hexo new page "categories"
```

修改文件代码 source/categories/index.md

```
title: 分类
date: 2021-10-15 15:09:46
type: categories
layout: categories
```

3.设置头像

在source新建文件夹images,添加avatar.jpg

```
# Sidebar Avatar
avatar:
  # Replace the default image and set the url here.
  url: /images/avatar.jpg
  # If true, the avatar will be dispalyed in circle.
  rounded: true
  # If true, the avatar will be rotated with the cursor.
  rotated: false
```



3.开启评论

* valine 设置enable: true
* 设置appid，appkey

4.添加统计





